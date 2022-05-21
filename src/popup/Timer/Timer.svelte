<script>
    import Button from './Button.svelte'

    let timerActionText = 'Start'
    let time

    function onStart() {
        chrome.storage.local.get(['isRunning'], (res) => {
            const isCurrentlyRunning = !res.isRunning
            chrome.storage.local.set(
                {
                    isRunning: isCurrentlyRunning,
                },
                () => {
                    timerActionText = isCurrentlyRunning ? 'Stop' : 'Start'
                }
            )
        })
    }

    function onReset() {
        chrome.storage.local.set(
            {
                timer: 0,
                isRunning: false,
            },
            () => {
                timerActionText = 'Start'
            }
        )
    }

    function updateTime() {
        chrome.storage.local.get(['timer'], (res) => {
            const minutes = `${Math.round(res.timer / 60)}`.padStart(2, '0')
            let seconds = '00'
            if (res.timer % 60 !== 0) {
                seconds = `${res.timer % 60}`.padStart(2, '0')
            }
            time = `${minutes}:${seconds}`
        })
    }
    updateTime()
    setInterval(updateTime, 1000)
</script>

<main>
    <div class="time">{time}</div>
    <div class="buttons-group">
        <Button on:click={onStart} text={timerActionText} bgColor={timerActionText === 'Stop' ? '#D9544F' : '#2B994A'} />
        <Button on:click={onReset} text="Reset" bgColor="#F8C01E" />
    </div>
</main>

<style>
    main {
        width: 350px;
        height: 200px;
        background-color: #838996;
        display: grid;
        justify-items: center;
        align-self: center;
    }
    .time {
        font-family: 'Neuton', sans-serif;
        margin-top: 1rem;
        font-size: 55px;
        color: #e2edea;
    }
    .buttons-group {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 1.5rem;
    }
</style>
