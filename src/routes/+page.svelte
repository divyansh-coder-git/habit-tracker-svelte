<script lang="ts">
  import { onMount } from "svelte";
  import moon_image from "./images/moon.png";
  import sun_image from "./images/brightness.png";
  import mental_health_image from "./images/mental-health.png";
  import pencil_image from "./images/pencil.png";
  import save_image from "./images/save.png";
  import cancel_image from "./images/close.png";

  import check from "./images/check.png";
  //   import trash_light from "./images/trash-light.png";
  //   import trash_dark from "./images/trash-dark.png";
  import trash_can from "./images/delete.png";
  import { fly } from "svelte/transition";

  interface Task {
    id: number;
    text: string;
    completed: boolean;
    createdAt: string;
    edited: boolean;
    editedAt: string;
  }

  let today = $state(new Date());

  let tasks: Task[] = $state([]);

  let newTaskText = $state("");

  onMount(() => {
    const saved = localStorage.getItem("tasks");

    if (saved) {
      tasks = JSON.parse(saved);
      if (localStorage.getItem("theme") == "dark") {
        isDark = true;
      } else {
        isDark = false;
      }
    } else {
    }
  });

  $effect(() => {
    localStorage.setItem("tasks", JSON.stringify(tasks));
    localStorage.setItem("theme", isDark ? "dark" : "light");
  });

  function addTask(event: Event) {
    event.preventDefault();
    if (!newTaskText.trim()) {
      return;
    }

    tasks = [
      ...tasks,
      {
        id: Date.now(),
        text: newTaskText,
        completed: false,
        createdAt: today.toLocaleDateString("en-GB", {
          day: "numeric",
          month: "short",
          year: "numeric",
        }),
        edited: false,
        editedAt: today.toLocaleDateString("en-GB", {
          day: "numeric",
          month: "short",
          year: "numeric",
        }),
      },
    ];

    newTaskText = "";
  }

  function deleteTask(id: number) {
    tasks = tasks.filter((tasks) => tasks.id !== id);
  }

  let total_task: number = $derived(tasks.length);
  let complete: number = $derived(
    tasks.filter((task) => task.completed).length,
  );

  let total_progess = $derived(
    total_task === 0 ? 0 : Math.floor((complete / total_task) * 100),
  );

  let isDark: boolean = $state(false);
  //   let theme_text: string = $derived(isDark ? "Light Mode" : "Dark Mode");
  let dynamic_image = $derived(isDark ? moon_image : sun_image);

  let editingId: number | null = $state(null);
  let editingText = $state("");

  function editTask(task: Task) {
    editingId = task.id;
    editingText = task.text;
  }

  function saveTask(task: Task) {
    if (!editingText.trim() || editingText == task.text) {
      return;
    }
    tasks = tasks.map((task) =>
      task.id === editingId
        ? {
            ...task,
            text: editingText,
            edited: true,
            editedAt: today.toLocaleDateString("en-GB", {
              day: "numeric",
              month: "short",
              year: "numeric",
            }),
          }
        : task,
    );

    editingId = null;
    editingText = "";
  }

  function cancelEdit() {
    editingId = null;
    editingText = "";
  }
</script>

<div
  class="flex py-5 justify-center min-h-screen"
  style:background-color={isDark ? "#333" : "#fff"}
  style:color={isDark ? "white" : "black"}
>
  <div
    class="w-full max-w-xl p-4 sm:p-8 rounded-3xl border border-zinc-600 {isDark
      ? 'shadow-xl shadow-white/50'
      : 'shadow-xl shadow-black/50'}"
  >
    <div class="flex justify-between">
      <div class="flex gap-5">
        <h1 class="text-3xl sm:text-4xl font-bold mb-2 inline">
          Habit Tracker
        </h1>
        <img class="w-15 h-auto" src={mental_health_image} alt="icon" />
      </div>

      <button
        class="transition-transform duration-300 ease-in-out hover:scale-120"
        onclick={() => (isDark = !isDark)}
        ><img class="w-8 sm:w-10" src={dynamic_image} alt="Icon" /></button
      >
    </div>

    <p class="text-gray-500 mb-6">Track your daily habits</p>
    <form class="flex flex-col sm:flex-row gap-2" onsubmit={addTask}>
      <input
        bind:value={newTaskText}
        type="text"
        placeholder="Add a new habit..."
        class="flex-1 px-4 py-3 placeholder-gray-400 rounded-xl border-2 border-gray-300 focus:border-green-500 focus:outline-none transition"
      />
      <button
        type="submit"
        class="px-6 sm:w-auto py-3 rounded-xl bg-green-600 text-white font-semibold hover:bg-green-500 transition"
        >Add</button
      >
    </form>

    <div
      class="mt-5 max-h-[37vh] sm:max-h-[40vh] overflow-y-auto pr-3 custom-scrollbar"
    >
      {#if tasks.length === 0}
        <p class="text-gray-500 mt-5 text-center w-full">
          No habits yet. Add one!
        </p>
      {/if}
      <ul>
        {#each tasks as task (task.id)}
          <li
            transition:fly={{ y: 20, duration: 100 }}
            class="flex items-center justify-between p-3 my-2 rounded-xl border hover:shadow-lg hover:shadow-green-500/5 transition-all duration-300 {task.completed
              ? 'border-green-500/5'
              : 'border-zinc-600'}"
          >
            {#if editingId === task.id}
              <form
                class="flex items-center gap-3 w-full"
                onsubmit={() => saveTask(task)}
              >
                <input
                  class="w-full px-1 py-1 placeholder-gray-400 rounded border-2 border-gray-300 focus:border-blue-500 focus:outline-none transition"
                  bind:value={editingText}
                />

                <button
                  type="submit"
                  class="ml-auto shrink-0 bg-none rounded py-0.5 px-0.5 transition-transform duration-300 ease-in-out hover:scale-130"
                  ><img class="w-4" src={save_image} alt="Edit Task" /></button
                >
                <button
                  class="ml-auto shrink-0 bg-none rounded py-0.5 px-0.5 transition-transform duration-300 ease-in-out hover:scale-130"
                  onclick={() => cancelEdit()}
                  ><img
                    class="w-4"
                    src={cancel_image}
                    alt="Edit Task"
                  /></button
                >
              </form>
            {:else}
              <div class="flex items-center gap-3 w-full">
                <input
                  type="checkbox"
                  bind:checked={task.completed}
                  class="transition-transform duration-300 ease-in-out hover:scale-130"
                />

                <div class="flex flex-col flex-1 min-w-0">
                  <span
                    class="flex-1 min-w-0 truncate"
                    title={task.text}
                    class:text-green-500={task.completed}
                    style:text-decoration={task.completed
                      ? "line-through"
                      : "none"}
                    style:opacity={task.completed ? 0.5 : 1}
                  >
                    {task.text}
                  </span>

                  <span class="text-xs opacity-60">
                    {task.edited ? "Edited" : "Added"}: {task.editedAt}
                  </span>
                </div>

                <button
                  class="ml-auto shrink-0 bg-none rounded py-0.5 px-0.5 transition-transform duration-300 ease-in-out hover:scale-140"
                  onclick={() => editTask(task)}
                  ><img
                    class="w-4"
                    src={pencil_image}
                    alt="Edit Task"
                  /></button
                >

                <button
                  class="ml-auto shrink-0 bg-none rounded py-0.5 px-0.5 transition-transform duration-300 ease-in-out hover:scale-130"
                  onclick={() => deleteTask(task.id)}
                  ><img class="w-5" src={trash_can} alt="Delete Task" /></button
                >
              </div>
            {/if}
          </li>
        {/each}
      </ul>
      {#if total_progess === 100 && total_task > 0}
        <div class="mt-4 p-3 rounded-xl bg-green-100 text-green-700">
          🎉 All habits completed today!
        </div>
      {/if}
    </div>
    <div class="flex justify-between mt-3">
      <p class="text-sm font-medium">Today's Progress</p>
      <p class="text-sm font-medium">{total_progess}%</p>
    </div>
    <div
      class="w-full mt-1 bg-gray-300 rounded-full h-4"
      class:bg-gray-700={isDark}
      class:bg-gray-300={!isDark}
    >
      <div
        class="bg-green-500 h-4 rounded-full transition-all duration-300"
        style={`width: ${total_progess}%`}
      ></div>
    </div>
    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mt-6">
      <div class="p-4 rounded-xl border-l-4 border-gray-300 text-center">
        <h2 class="text-3xl font-bold">{total_task}</h2>
        <p>Total</p>
      </div>

      <div class="p-4 rounded-xl border-l-4 border-green-600 text-center">
        <h2 class="text-3xl font-bold">{complete}</h2>
        <p>Done</p>
      </div>

      <div class="p-4 rounded-xl border-l-4 border-blue-600 text-center">
        <h2 class="text-3xl font-bold">
          {total_progess}%
        </h2>
        <p>Progress</p>
      </div>
    </div>
  </div>
</div>

<style>
  .custom-scrollbar::-webkit-scrollbar {
    width: 8px;
  }

  .custom-scrollbar::-webkit-scrollbar-track {
    background: transparent;
  }

  .custom-scrollbar::-webkit-scrollbar-thumb {
    background: #4ade80;
    border-radius: 9999px;
  }
</style>
