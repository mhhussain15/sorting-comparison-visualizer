const quickSortCanvas = document.getElementById('quickSortCanvas');
const bubbleSortCanvas = document.getElementById('bubbleSortCanvas');
const selectionSortCanvas = document.getElementById('selectionSortCanvas');

const quickSortCtx = quickSortCanvas.getContext('2d');
const bubbleSortCtx = bubbleSortCanvas.getContext('2d');
const selectionSortCtx = selectionSortCanvas.getContext('2d');

const canvasWidth = 300;
const canvasHeight = 400;

function drawArray(ctx, arr, color) {
    const barWidth = canvasWidth / arr.length;
    const barHeightUnit = canvasHeight / Math.max(...arr);

    ctx.clearRect(0, 0, canvasWidth, canvasHeight);
    ctx.fillStyle = color || '#3498db';

    for (let i = 0; i < arr.length; i++) {
        const barHeight = arr[i] * barHeightUnit;
        ctx.fillRect(i * barWidth, canvasHeight - barHeight, barWidth, barHeight);
    }
}

async function bubbleSort(arr, ctx) {
    const n = arr.length;
    for (let i = 0; i < n - 1; i++) {
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
                drawArray(ctx, arr, '#e74c3c');
                await sleep(10);
            }
        }
    }
}

async function selectionSort(arr, ctx) {
    const n = arr.length;
    for (let i = 0; i < n - 1; i++) {
        let minIndex = i;
        for (let j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        [arr[i], arr[minIndex]] = [arr[minIndex], arr[i]];
        drawArray(ctx, arr, '#2ecc71');
        await sleep(10);
    }
}

async function quickSort(arr, ctx, left = 0, right = arr.length - 1) {
    if (left < right) {
        const pivotIndex = await partition(arr, left, right, ctx);
        await Promise.all([
            quickSort(arr, ctx, left, pivotIndex - 1),
            quickSort(arr, ctx, pivotIndex + 1, right)
        ]);
    }
    return arr;
}

async function partition(arr, left, right, ctx) {
    const pivot = arr[right];
    let i = left - 1;
    for (let j = left; j < right; j++) {
        if (arr[j] < pivot) {
            i++;
            [arr[i], arr[j]] = [arr[j], arr[i]];
            drawArray(ctx, arr, '#f39c12');
            await sleep(10);
        }
    }
    [arr[i + 1], arr[right]] = [arr[right], arr[i + 1]];
    drawArray(ctx, arr, '#f39c12');
    await sleep(10);
    return i + 1;
}

function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function startSorting() {
    const array = Array.from({ length: 50 }, () => Math.floor(Math.random() * 100) + 1);
    drawArray(quickSortCtx, array.slice(), '#f39c12');
    drawArray(bubbleSortCtx, array.slice(), '#e74c3c');
    drawArray(selectionSortCtx, array.slice(), '#2ecc71');

    await Promise.all([
        bubbleSort(array.slice(), bubbleSortCtx),
        selectionSort(array.slice(), selectionSortCtx),
        quickSort(array.slice(), quickSortCtx)
    ]);
}
startSorting();
