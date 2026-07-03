# 🎯 Habit Tracker

A modern, responsive web application for tracking daily habits built with **Svelte** and **SvelteKit**. Stay motivated by visualizing your progress with an intuitive interface that supports dark mode and persistent local storage.

![Svelte](https://img.shields.io/badge/Svelte-5-orange?logo=svelte)
![TypeScript](https://img.shields.io/badge/TypeScript-6-blue?logo=typescript)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-4-blue?logo=tailwindcss)
![License](https://img.shields.io/badge/License-MIT-green)

---

## ✨ Features

- **📝 Add & Manage Habits** - Create new habits and organize them in a clean interface
- **✅ Track Completion** - Mark habits as complete with checkboxes
- **📊 Progress Tracking** - Visual progress bar showing daily completion percentage
- **🌙 Dark Mode** - Toggle between light and dark themes
- **✏️ Edit Habits** - Modify habit text with save/cancel functionality
- **🗑️ Delete Habits** - Remove habits you no longer need
- **💾 Local Storage** - Your habits and theme preference persist across sessions
- **🎨 Responsive Design** - Works seamlessly on desktop, tablet, and mobile
- **⌚ Timestamps** - Track when habits were created and last edited
- **🎉 Motivation** - Celebrate when all daily habits are completed!

---

## 🛠️ Tech Stack

- **Frontend Framework**: [Svelte 5](https://svelte.dev) - Reactive, lightweight UI
- **Build Tool**: [Vite](https://vitejs.dev) - Fast bundling and dev server
- **Styling**: [Tailwind CSS 4](https://tailwindcss.com) - Utility-first CSS framework
- **Language**: [TypeScript](https://www.typescriptlang.org) - Type-safe development
- **Adapter**: [SvelteKit Auto Adapter](https://svelte.dev/docs/kit/adapters)

---

## 📁 Project Structure

```
habit-tracker-svelte/
├── src/
│   ├── lib/
│   │   ├── Components/       # Reusable Svelte components
│   │   ├── assets/          # Static assets (images, icons)
│   │   └── index.ts         # Library exports
│   ├── routes/
│   │   ├── +page.svelte     # Main application page
│   │   └── images/          # Route-specific images
│   ├── app.html             # HTML entry point
│   └── app.d.ts             # TypeScript definitions
├── static/                   # Static files served as-is
├── package.json             # Project dependencies
├── svelte.config.js         # Svelte configuration
├── vite.config.ts           # Vite configuration
└── tsconfig.json            # TypeScript configuration
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js 16+ 
- npm, yarn, or pnpm package manager

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/divyansh-coder-git/habit-tracker-svelte.git
   cd habit-tracker-svelte
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

   The application will be available at `http://localhost:5173` (or the next available port)

4. **Open in browser** (optional - Vite shows the URL in terminal)
   ```bash
   npm run dev -- --open
   ```

---

## 📦 Available Scripts

```bash
# Development server with hot reload
npm run dev

# Build for production
npm run build

# Preview production build locally
npm run preview

# Type check and Svelte sync
npm run check

# Watch for type errors
npm run check:watch
```

---

## 🎯 How to Use

1. **Add a Habit** - Type the habit name in the input field and click "Add" or press Enter
2. **Track Progress** - Check the box next to a habit to mark it as complete
3. **Edit Habit** - Click the pencil icon to edit the habit text
4. **Save/Cancel** - Use save/cancel icons when editing
5. **Delete Habit** - Click the trash icon to remove a habit
6. **Toggle Theme** - Click the sun/moon icon in the top-right corner for dark mode
7. **View Stats** - See your daily progress with the percentage bar and statistics cards

---

## 💾 Data Persistence

Your habits and theme preference are automatically saved to browser's `localStorage`:
- **tasks** - Array of all habits with completion status
- **theme** - Current theme preference (light/dark)

Data persists even after closing the browser tab!

---

## 🎨 UI Components

### Main Features Displayed:
- **Header** - Title, theme toggle, and mental health icon
- **Input Form** - Add new habits
- **Habit List** - Scrollable list with edit/delete controls
- **Progress Bar** - Visual completion percentage
- **Statistics Cards** - Total habits, completed, and progress percentage

---

## 🔄 Task Interface

```typescript
interface Task {
  id: number;           // Unique identifier (timestamp)
  text: string;         // Habit description
  completed: boolean;   // Completion status
  createdAt: string;    // Creation date
  edited: boolean;      // Whether habit was edited
  editedAt: string;     // Last edit date
}
```

---

## 📱 Responsive Breakpoints

- **Mobile** - Optimized layout for phones (< 640px)
- **Tablet** - Medium layout adjustments (640px - 1024px)
- **Desktop** - Full-featured layout (> 1024px)

---

## 🌙 Dark Mode

Theme preference is remembered and applied on page load. The app detects and respects your system theme preference on first visit.

---

## 🎉 Special Features

- **Celebration Message** - When you complete all daily habits, a celebratory message appears
- **Smooth Animations** - Fly-in transitions when adding/removing habits
- **Hover Effects** - Interactive buttons with scale transformations
- **Custom Scrollbar** - Styled green scrollbar for the task list

---

## 🔮 Future Enhancement Ideas

- 📅 Multi-day/week/month tracking
- 📊 Historical data and statistics
- 🔔 Browser notifications for reminders
- 🎨 Customizable colors and themes
- ☁️ Cloud sync across devices
- 📈 Streak tracking

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 🤝 Contributing

Contributions are welcome! Feel free to:
1. Fork the repository
2. Create a new branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 🐛 Issues & Bug Reports

Found a bug? Please [open an issue](https://github.com/divyansh-coder-git/habit-tracker-svelte/issues) with:
- Detailed description
- Steps to reproduce
- Expected vs actual behavior
- Browser and OS information

---

## 💬 Feedback

Have suggestions? Open a discussion or issue - I'd love to hear your ideas!

---

## 👤 Author

**Divyansh** - [@divyansh-coder-git](https://github.com/divyansh-coder-git)

---

## 📚 Resources

- [Svelte Documentation](https://svelte.dev/docs)
- [SvelteKit Guide](https://svelte.dev/docs/kit)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [Vite Guide](https://vitejs.dev/guide/)

---

**Happy Habit Building! 🚀**
