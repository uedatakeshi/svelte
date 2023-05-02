<!-- App.svelte -->
<script>
  import { onMount } from "svelte";

  let diary = {
    weather: "",
    manager: "",
    sleep_time: "",
    start: "",
    end: "",
    comment: "",
  };
  let isEditing = false;
  let fetchError = null;

  // APIのURL
  const showUrl = "http://127.0.0.1:8000/api/diaries/show/1";
  const updateUrl = "http://127.0.0.1:8000/api/diaries/update/1";

  // APIを呼び出して日記を取得する関数
  const getDiary = async () => {
    try {
      const response = await fetch(showUrl);
      const data = await response.json();
      diary = data;
    } catch (error) {
      fetchError = error;
    }
  };

  // フォームを送信して日記を更新する関数
  const updateDiary = async () => {
    try {
      const response = await fetch(updateUrl, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(diary),
      });
      const data = await response.json();
      isEditing = false;
      getDiary();
    } catch (error) {
      fetchError = error;
    }
  };

  // ページが読み込まれたらAPIから日記を取得する
  onMount(() => {
    getDiary();
  });
</script>

<main>
  {#if fetchError}

    <p>Error: {fetchError.message}</p>
  
  {:else if isEditing}

  <!-- 編集用フォーム -->
    <form on:submit|preventDefault={updateDiary}>
      <label>
        Weather:
        <input type="text" bind:value={diary.weather} />
      </label>
      <label>
        Manager:
        <input type="text" bind:value={diary.manager} />
      </label>
      <label>
        Sleep Time:
        <input type="text" bind:value={diary.sleep_time} />
      </label>
      <label>
        Start:
        <input type="text" bind:value={diary.start} />
      </label>
      <label>
        End:
        <input type="text" bind:value={diary.end} />
      </label>
      <label>
        Comment:
        <input type="text" bind:value={diary.comment} />
      </label>
      <button type="submit">Update</button>
      <button on:click={() => (isEditing = false)}>Cancel</button>
    </form>

  {:else}

  <!-- 表示用 -->
    <div>
      <p>Weather: {diary.weather}</p>
      <p>Manager: {diary.manager}</p>
      <p>Sleep Time: {diary.sleep_time}</p>
      <p>Start: {diary.start}</p>
      <p>End: {diary.end}</p>
      <p>Comment: {diary.comment}</p>
      <button on:click={() => (isEditing = true)}>Edit</button>
    </div>
  {/if}
</main>

<style>
  /* 必要なCSSをここに記述してください */
</style>
