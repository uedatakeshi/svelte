<!-- DiaryDisplay.svelte -->
<script>
    let weather = '';
    let manager = '';
    let sleep_time = '';
    let start = '';
    let end = '';
    let comment = '';
  
    async function loadData() {
      const response = await fetch('http://127.0.0.1:8000/api/diaries/show/1');
      const data = await response.json();
      weather = data.weather;
      manager = data.manager;
      sleep_time = data.sleep_time;
      start = data.start;
      end = data.end;
      comment = data.comment;
    }
  
    loadData();
  </script>
  
  <div>
    <h2>日記</h2>
  
    <label>天気: {weather}</label>
    <label>担当者: {manager}</label>
    <label>睡眠時間: {sleep_time}</label>
    <label>開始時: {start}</label>
    <label>終了時: {end}</label>
    <label>メモ: {comment}</label>
  
    <button on:click={() => window.history.back()}>戻る</button>
  </div>
  