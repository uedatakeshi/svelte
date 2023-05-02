<script>
    export let diary;
</script>

        <div>
            <div className='mb-3'>
                <label className='form-label'>天気</label>
                <p className='h3 bg-light p-3'>{diary.weather}</p>
            </div>
            <div className="mb-3">
                <label className="form-label">担当者</label>
                <p className="h3 bg-light p-3">{diary.manager}</p>
            </div>
            <div className="mb-3">
                <label className="form-label">睡眠時間</label>
                <p className="h3 bg-light p-3">{diary.sleep_time}時間</p>
            </div>
            <div className="mb-3">
                <label className="form-label">出社時間</label>
                <p className="h3 bg-light p-3">{diary.start}～{diary.end}</p>
            </div>
            <div className="mb-3">
                <label className="form-label">コメント</label>
                <p className="h3 bg-light p-3">{diary.comment}</p>
            </div>

        </div>