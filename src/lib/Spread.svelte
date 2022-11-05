<script lang="ts">
    let n: number;
    let res: any = "";
    let ready: boolean = false;

    const handleSubmit = () => {
        let num = Number(n);
        if (!Number.isFinite(num) || num % 4 !== 0) {
            res = "Invalid Input";
            return;
        }
        let temp: string[] = [];
        let half = num / 2;
        let left = 2;
        let right = num;
        for (let i = 0; i < half; i += 2) {
            temp.push(left.toString());
            left++;
            temp.push(left.toString());
            left += 3;
        }

        for (let j = 0; j < half; j += 2) {
            temp.push(right.toString());
            right -= 3;
            temp.push(right.toString());
            right--;
        }
        ready = true;
        res = temp.toString();
    };

    const handleClipboard = () => {
        navigator.clipboard.writeText(res.toString());
    };
</script>

<div class=" bg-stone-300 flex flex-col h-screen">
    <div class="h-full w-full flex justify-around items-end p-4">
        <form on:submit|preventDefault={handleSubmit}>
            <input
                type="text"
                bind:value={n}
                class="bg-stone-100 bg-opacity-50 rounded border focus:border-slate-500 focus:bg-transparent focus:ring-1 focus:ring-slate-500 text-base outline-none p-1 leading-8 transition-colors duration-200 ease-in-out"
            />
            <button
                class=" text-white bg-slate-500 border-0 p-1 focus:outline-none hover:bg-slate-600 rounded"
                type="submit"
            >
                Submit
            </button>
        </form>
    </div>
    <div class="h-full w-full flex flex-col justify-center items-center">
        <div class="h-10 w-full flex flex-col justify-center items-center">
            <h1 class="text-ellipsis overflow-hidden">{res}</h1>
        </div>
        <div class="h-full w-full flex flex-col justify-start items-center m-4">
            {#if ready}
                <button
                    class=" text-white bg-slate-500 border-0 p-1 focus:outline-none hover:bg-slate-600 rounded"
                    on:click={handleClipboard}>Copy To Clipboard</button
                >
            {/if}
        </div>
    </div>
</div>

<style>
</style>
