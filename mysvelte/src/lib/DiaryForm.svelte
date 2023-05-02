<!-- DiaryForm.svelte -->
<script>
  let weather = '';
  let manager = '';
  let sleep_time = '';
  let start = '';
  let end = '';
  let comment = '';

  async function submitForm() {
    const data = {
      weather,
      manager,
      sleep_time,
      start,
      end,
      comment,
    };
    const response = await fetch('http://127.0.0.1:8000/api/diaries/update/1', {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(data),
    });
    const result = await response.json();
    console.log(result);
  }
</script>

<div>
  <label for="weather">天気:</label>
  <input id="weather" bind:value={weather} />

  <label for="manager">担当者:</label>
  <input id="manager" bind:value={manager} />

  <label for="sleep_time">睡眠時間:</label>
  <input id="sleep_time" bind:value={sleep_time} />

  <label for="start">開始時:</label>
  <input id="start" bind:value={start} />

  <label for="end">終了時:</label>
  <input id="end" bind:value={end} />

  <label for="comment">メモ:</label>
  <textarea id="comment" bind:value={comment}></textarea>

  <button on:click={submitForm}>登録</button>
  <button on:click={() => window.history.back()}>戻る</button>
</div>
