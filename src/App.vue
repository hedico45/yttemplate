<script setup>
    import {ref, computed, reactive} from 'vue' 
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'

const urlVideo = ref('')
const referer = ref('')
const name =ref('')
const format = ref('')
const formats = ref(false)
const limit = ref(false)
const rate = ref(180)
const setFormat = ref(false)
const ytdlp = computed(() => {
    return 'yt-dlp '+option1.value+' --user-agent "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36"'+refererValue.value+urlValue.value+ nameValue.value;
});

function changeFormats() {
    formats.value = !formats.value;
}

function changeLimit() {
    limit.value = !limit.value;
}

function changeSetFormat() {
    setFormat.value = !setFormat.value;
}

const option1 = computed(() => {
    let text = limit.value ? '--rate-limit '+rate.value+'k --cache-dir --continue' : '--cache-dir --continue';
    let text2 = !setFormat.value ? '-f "' + format.value + '" ' : '';
    return formats.value ? text2 + text : '--list-formats';
})

const nameValue = computed(() => {
    return name.value ? ' -o "' + name.value + '.mp4"' : '';
})

const refererValue = computed(() => {
    return referer.value ? ' --referer "' + referer.value + '" ' : '';
})

const urlValue = computed(() => {
    return urlVideo.value ? ' "' + urlVideo.value + '" ' : '';
})

</script>
<template>
    <main>
        <div class="flex flex-row justify-center items-center h-screen w-screen max-w-full">
            <div class="form-control flex-1 mx-10 gap-10 flex">
                <div class="flex flex-row justify-between">
                    <label class="label cursor-pointer gap-3">
                        <span class="label-text">List Formats</span>
                        <input @click="changeFormats" type="checkbox" checked="checked" class="checkbox checkbox-primary" />
                    </label>
                    <label class="label cursor-pointer gap-3">
                        <span class="label-text">Format</span>
                        <input @click="changeSetFormat" type="checkbox" checked="checked" class="checkbox checkbox-primary" />
                        <input v-model="format" type="text" placeholder="format" class="
                                input input-primary input-bordered
                            " />
                    </label>
                    <label class="label cursor-pointer gap-3">
                        <span class="label-text">Rate Limit</span>
                        <input @click="changeLimit" type="checkbox" class="checkbox checkbox-primary" />
                        <input v-model="rate" type="text" placeholder="rate" class="
                                input input-primary input-bordered
                            " />
                        <span>Kb/s</span>
                    </label>
                </div>
                <label class="input-group">URL
                    <input v-model="urlVideo" type="text" placeholder="enter url video" class="
                                w-full
                                pr-16
                                input input-primary input-bordered
                            " />
                </label>
                <label class="input-group">Referer
                    <input v-model="referer" type="text" placeholder="enter referer video" class="
                                w-full
                                pr-16
                                input input-primary input-bordered
                            " />
                </label>
                <label class="input-group">Nombre
                    <input v-model="name" type="text" placeholder="enter referer video" class="
                                w-full
                                pr-16
                                input input-primary input-bordered
                            " />
                </label>
                <label class="input-group">Salida
                    <textarea class="textarea textarea-primary w-full h-full" placeholder="" v-model="ytdlp"></textarea>
                </label>
            </div>
        </div>
    </main>
</template>
<style scoped>
</style>