# Building Your First App

## Project Overview

In this tutorial, we'll build a **Task Manager CLI Application** using TypeScript. This project demonstrates:

- TypeScript fundamentals in practice
- File system operations
- Command-line interfaces
- JSON data persistence
- Project organization

## Project Setup

### 1. Initialize the Project

```bash
mkdir task-manager
cd task-manager

# Initialize npm and TypeScript
npm init -y
npm install typescript ts-node @types/node --save-dev
npx tsc --init
```

### 2. Configure TypeScript

Update `tsconfig.json`:

```json
{
    "compilerOptions": {
        "target": "ES2020",
        "module": "commonjs",
        "outDir": "./dist",
        "rootDir": "./src",
        "strict": true,
        "esModuleInterop": true,
        "skipLibCheck": true,
        "forceConsistentCasingInFileNames": true,
        "resolveJsonModule": true
    },
    "include": ["src/**/*"],
    "exclude": ["node_modules"]
}
```

### 3. Create Project Structure

```bash
mkdir src
mkdir src/models
mkdir src/services
mkdir data
```

Structure:
```
task-manager/
├── src/
│   ├── index.ts          # Entry point
│   ├── models/
│   │   └── Task.ts       # Task interface/class
│   └── services/
│       └── TaskService.ts # Business logic
├── data/
│   └── tasks.json        # Data storage
├── package.json
└── tsconfig.json
```

## Building the Application

### Step 1: Define the Task Model

Create `src/models/Task.ts`:

```typescript
export interface Task {
    id: number;
    title: string;
    description: string;
    completed: boolean;
    priority: 'low' | 'medium' | 'high';
    createdAt: Date;
    completedAt?: Date;
}

export type CreateTaskInput = {
    title: string;
    description?: string;
    priority?: Task['priority'];
};

export type UpdateTaskInput = Partial<Omit<Task, 'id' | 'createdAt'>>;
```

### Step 2: Create the Task Service

Create `src/services/TaskService.ts`:

```typescript
import * as fs from 'fs';
import * as path from 'path';
import { Task, CreateTaskInput, UpdateTaskInput } from '../models/Task';

export class TaskService {
    private tasks: Task[] = [];
    private dataPath: string;

    constructor() {
        this.dataPath = path.join(process.cwd(), 'data', 'tasks.json');
        this.loadTasks();
    }

    // Load tasks from file
    private loadTasks(): void {
        try {
            if (fs.existsSync(this.dataPath)) {
                const data = fs.readFileSync(this.dataPath, 'utf-8');
                const parsed = JSON.parse(data);
                this.tasks = parsed.map((task: any) => ({
                    ...task,
                    createdAt: new Date(task.createdAt),
                    completedAt: task.completedAt ? new Date(task.completedAt) : undefined
                }));
            }
        } catch (error) {
            console.error('Error loading tasks:', error);
            this.tasks = [];
        }
    }

    // Save tasks to file
    private saveTasks(): void {
        try {
            const dir = path.dirname(this.dataPath);
            if (!fs.existsSync(dir)) {
                fs.mkdirSync(dir, { recursive: true });
            }
            fs.writeFileSync(this.dataPath, JSON.stringify(this.tasks, null, 2));
        } catch (error) {
            console.error('Error saving tasks:', error);
        }
    }

    // Generate next ID
    private getNextId(): number {
        if (this.tasks.length === 0) return 1;
        return Math.max(...this.tasks.map(t => t.id)) + 1;
    }

    // Create a new task
    create(input: CreateTaskInput): Task {
        const task: Task = {
            id: this.getNextId(),
            title: input.title,
            description: input.description || '',
            completed: false,
            priority: input.priority || 'medium',
            createdAt: new Date()
        };

        this.tasks.push(task);
        this.saveTasks();
        return task;
    }

    // Get all tasks
    getAll(): Task[] {
        return [...this.tasks];
    }

    // Get task by ID
    getById(id: number): Task | undefined {
        return this.tasks.find(t => t.id === id);
    }

    // Get tasks by status
    getByStatus(completed: boolean): Task[] {
        return this.tasks.filter(t => t.completed === completed);
    }

    // Get tasks by priority
    getByPriority(priority: Task['priority']): Task[] {
        return this.tasks.filter(t => t.priority === priority);
    }

    // Update a task
    update(id: number, input: UpdateTaskInput): Task | undefined {
        const index = this.tasks.findIndex(t => t.id === id);
        if (index === -1) return undefined;

        const task = this.tasks[index];
        const updated: Task = {
            ...task,
            ...input,
            completedAt: input.completed ? new Date() : task.completedAt
        };

        this.tasks[index] = updated;
        this.saveTasks();
        return updated;
    }

    // Toggle task completion
    toggleComplete(id: number): Task | undefined {
        const task = this.getById(id);
        if (!task) return undefined;

        return this.update(id, {
            completed: !task.completed,
            completedAt: !task.completed ? new Date() : undefined
        });
    }

    // Delete a task
    delete(id: number): boolean {
        const index = this.tasks.findIndex(t => t.id === id);
        if (index === -1) return false;

        this.tasks.splice(index, 1);
        this.saveTasks();
        return true;
    }

    // Clear completed tasks
    clearCompleted(): number {
        const initialCount = this.tasks.length;
        this.tasks = this.tasks.filter(t => !t.completed);
        this.saveTasks();
        return initialCount - this.tasks.length;
    }

    // Get statistics
    getStats(): {
        total: number;
        completed: number;
        pending: number;
        byPriority: Record<Task['priority'], number>;
    } {
        const completed = this.tasks.filter(t => t.completed).length;
        const byPriority = {
            low: this.tasks.filter(t => t.priority === 'low').length,
            medium: this.tasks.filter(t => t.priority === 'medium').length,
            high: this.tasks.filter(t => t.priority === 'high').length
        };

        return {
            total: this.tasks.length,
            completed,
            pending: this.tasks.length - completed,
            byPriority
        };
    }
}
```

### Step 3: Create the CLI Interface

Create `src/index.ts`:

```typescript
import * as readline from 'readline';
import { TaskService } from './services/TaskService';
import { Task } from './models/Task';

const taskService = new TaskService();

// Create readline interface
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Helper to prompt user
function prompt(question: string): Promise<string> {
    return new Promise(resolve => {
        rl.question(question, answer => {
            resolve(answer.trim());
        });
    });
}

// Display a task
function displayTask(task: Task): void {
    const status = task.completed ? '✓' : '○';
    const priorityEmoji = {
        high: '🔴',
        medium: '🟡',
        low: '🟢'
    };

    console.log(`
  ${status} [${task.id}] ${task.title}
     ${priorityEmoji[task.priority]} Priority: ${task.priority}
     📝 ${task.description || 'No description'}
     📅 Created: ${task.createdAt.toLocaleDateString()}
     ${task.completedAt ? `✅ Completed: ${task.completedAt.toLocaleDateString()}` : ''}
    `.trim());
}

// Display all tasks
function displayTasks(tasks: Task[]): void {
    if (tasks.length === 0) {
        console.log('\n  No tasks found.\n');
        return;
    }

    console.log('\n--- Tasks ---');
    tasks.forEach(displayTask);
    console.log('-------------\n');
}

// Show help menu
function showHelp(): void {
    console.log(`
╔════════════════════════════════════════╗
║         Task Manager Commands          ║
╠════════════════════════════════════════╣
║  add      - Add a new task             ║
║  list     - Show all tasks             ║
║  pending  - Show pending tasks         ║
║  done     - Show completed tasks       ║
║  complete - Mark task as complete      ║
║  delete   - Delete a task              ║
║  clear    - Clear completed tasks      ║
║  stats    - Show statistics            ║
║  help     - Show this menu             ║
║  exit     - Exit the application       ║
╚════════════════════════════════════════╝
    `);
}

// Show statistics
function showStats(): void {
    const stats = taskService.getStats();
    console.log(`
╔═══════════════════════════════════════╗
║            Task Statistics            ║
╠═══════════════════════════════════════╣
║  Total tasks:      ${String(stats.total).padStart(3)}               ║
║  Completed:        ${String(stats.completed).padStart(3)}               ║
║  Pending:          ${String(stats.pending).padStart(3)}               ║
╠═══════════════════════════════════════╣
║  By Priority:                         ║
║    🔴 High:        ${String(stats.byPriority.high).padStart(3)}               ║
║    🟡 Medium:      ${String(stats.byPriority.medium).padStart(3)}               ║
║    🟢 Low:         ${String(stats.byPriority.low).padStart(3)}               ║
╚═══════════════════════════════════════╝
    `);
}

// Add task command
async function addTask(): Promise<void> {
    const title = await prompt('  Title: ');
    if (!title) {
        console.log('  ❌ Title is required.\n');
        return;
    }

    const description = await prompt('  Description (optional): ');
    const priorityInput = await prompt('  Priority (low/medium/high) [medium]: ');

    let priority: Task['priority'] = 'medium';
    if (['low', 'medium', 'high'].includes(priorityInput)) {
        priority = priorityInput as Task['priority'];
    }

    const task = taskService.create({ title, description, priority });
    console.log(`\n  ✅ Task created with ID: ${task.id}\n`);
}

// Complete task command
async function completeTask(): Promise<void> {
    const idInput = await prompt('  Task ID to complete: ');
    const id = parseInt(idInput, 10);

    if (isNaN(id)) {
        console.log('  ❌ Invalid ID.\n');
        return;
    }

    const task = taskService.toggleComplete(id);
    if (task) {
        const status = task.completed ? 'completed' : 'marked as pending';
        console.log(`\n  ✅ Task ${id} ${status}.\n`);
    } else {
        console.log(`\n  ❌ Task ${id} not found.\n`);
    }
}

// Delete task command
async function deleteTask(): Promise<void> {
    const idInput = await prompt('  Task ID to delete: ');
    const id = parseInt(idInput, 10);

    if (isNaN(id)) {
        console.log('  ❌ Invalid ID.\n');
        return;
    }

    const confirm = await prompt(`  Delete task ${id}? (y/n): `);
    if (confirm.toLowerCase() !== 'y') {
        console.log('  Cancelled.\n');
        return;
    }

    if (taskService.delete(id)) {
        console.log(`\n  ✅ Task ${id} deleted.\n`);
    } else {
        console.log(`\n  ❌ Task ${id} not found.\n`);
    }
}

// Clear completed tasks
async function clearCompleted(): Promise<void> {
    const confirm = await prompt('  Clear all completed tasks? (y/n): ');
    if (confirm.toLowerCase() !== 'y') {
        console.log('  Cancelled.\n');
        return;
    }

    const count = taskService.clearCompleted();
    console.log(`\n  ✅ Cleared ${count} completed task(s).\n`);
}

// Main application loop
async function main(): Promise<void> {
    console.log('\n🗂️  Welcome to Task Manager!\n');
    showHelp();

    while (true) {
        const command = await prompt('> ');

        switch (command.toLowerCase()) {
            case 'add':
                await addTask();
                break;

            case 'list':
                displayTasks(taskService.getAll());
                break;

            case 'pending':
                displayTasks(taskService.getByStatus(false));
                break;

            case 'done':
                displayTasks(taskService.getByStatus(true));
                break;

            case 'complete':
                await completeTask();
                break;

            case 'delete':
                await deleteTask();
                break;

            case 'clear':
                await clearCompleted();
                break;

            case 'stats':
                showStats();
                break;

            case 'help':
                showHelp();
                break;

            case 'exit':
            case 'quit':
                console.log('\n👋 Goodbye!\n');
                rl.close();
                process.exit(0);

            default:
                if (command) {
                    console.log(`  Unknown command: ${command}`);
                    console.log('  Type "help" for available commands.\n');
                }
        }
    }
}

// Start the application
main().catch(console.error);
```

### Step 4: Add npm Scripts

Update `package.json`:

```json
{
    "name": "task-manager",
    "version": "1.0.0",
    "description": "CLI Task Manager built with TypeScript",
    "main": "dist/index.js",
    "scripts": {
        "build": "tsc",
        "start": "node dist/index.js",
        "dev": "ts-node src/index.ts"
    },
    "devDependencies": {
        "@types/node": "^20.0.0",
        "ts-node": "^10.0.0",
        "typescript": "^5.0.0"
    }
}
```

## Running the Application

```bash
# Development mode (with ts-node)
npm run dev

# Production mode
npm run build
npm start
```

## Using the Application

```
🗂️  Welcome to Task Manager!

> add
  Title: Learn TypeScript
  Description (optional): Complete the tutorial series
  Priority (low/medium/high) [medium]: high

  ✅ Task created with ID: 1

> add
  Title: Build a project
  Description (optional): Apply what I learned
  Priority (low/medium/high) [medium]: medium

  ✅ Task created with ID: 2

> list

--- Tasks ---
  ○ [1] Learn TypeScript
     🔴 Priority: high
     📝 Complete the tutorial series
     📅 Created: 1/15/2024

  ○ [2] Build a project
     🟡 Priority: medium
     📝 Apply what I learned
     📅 Created: 1/15/2024
-------------

> complete
  Task ID to complete: 1

  ✅ Task 1 completed.

> stats

╔═══════════════════════════════════════╗
║            Task Statistics            ║
╠═══════════════════════════════════════╣
║  Total tasks:        2               ║
║  Completed:          1               ║
║  Pending:            1               ║
╠═══════════════════════════════════════╣
║  By Priority:                         ║
║    🔴 High:          1               ║
║    🟡 Medium:        1               ║
║    🟢 Low:           0               ║
╚═══════════════════════════════════════╝

> exit

👋 Goodbye!
```

## Enhancements to Try

Once you have the basic app working, try adding these features:

### 1. Due Dates
```typescript
interface Task {
    // ... existing properties
    dueDate?: Date;
}
```

### 2. Search Function
```typescript
search(query: string): Task[] {
    const lower = query.toLowerCase();
    return this.tasks.filter(t =>
        t.title.toLowerCase().includes(lower) ||
        t.description.toLowerCase().includes(lower)
    );
}
```

### 3. Categories/Tags
```typescript
interface Task {
    // ... existing properties
    tags: string[];
}
```

### 4. Export to Markdown
```typescript
exportToMarkdown(): string {
    let md = '# Tasks\n\n';
    for (const task of this.tasks) {
        const checkbox = task.completed ? '[x]' : '[ ]';
        md += `- ${checkbox} ${task.title}\n`;
    }
    return md;
}
```

## What You Learned

- **Project Setup**: Creating a TypeScript project from scratch
- **Interfaces**: Defining data structures with TypeScript
- **Classes**: Encapsulating business logic
- **File System**: Reading and writing JSON files
- **Async/Await**: Handling user input asynchronously
- **Type Safety**: Using TypeScript to prevent bugs

## Next Steps

Now that you've built your first app, explore:

1. **Web Apps**: Try React, Vue, or Angular with TypeScript
2. **APIs**: Build a REST API with Express or Fastify
3. **Databases**: Connect to MongoDB, PostgreSQL, or SQLite
4. **Testing**: Add unit tests with Jest
5. **Deployment**: Package and deploy your application

---

**Previous:** [[15 - Development Environment Setup]]

**Back to:** [[00 - Welcome]]

---

> [!success] Congratulations!
> You've completed the TypeScript & JavaScript tutorial series! Keep practicing by building more projects and exploring the ecosystem.
