<script setup lang="ts">
import { Head, Link } from '@inertiajs/vue3';
import { ref, reactive } from 'vue';

const event = ref('請輸入待辦事項');
const events = reactive(new Array());
const addEvent = () => {
    events.push(event.value);
    event.value = '';
    console.log(events);
}
const del=(idx)=>{
    events.splice(idx,1);
}

</script>

<template>

    <Head title="Welcome">
        <link rel="preconnect" href="https://rsms.me/" />
        <link rel="stylesheet" href="https://rsms.me/inter/inter.css" />
    </Head>
    <div
        class="flex min-h-screen flex-col items-center bg-[#FDFDFC] mt-6 text-[#1b1b18] dark:bg-[#0a0a0a] lg:justify-center lg:p-8">
        <header class="not-has-[nav]:hidden mb-6 w-full max-w-[335px] text-sm lg:max-w-4xl">
            <nav class="flex items-center justify-end gap-4">
                <Link v-if="$page.props.auth.user" :href="route('dashboard')"
                    class="inline-block rounded-sm border border-[#19140035] px-5 py-1.5 text-sm leading-normal text-[#1b1b18] hover:border-[#1915014a] dark:border-[#3E3E3A] dark:text-[#EDEDEC] dark:hover:border-[#62605b]">
                Dashboard
                </Link>
                <template v-else>
                    <Link :href="route('login')"
                        class="inline-block rounded-sm border border-transparent px-5 py-1.5 text-sm leading-normal text-[#1b1b18] hover:border-[#19140035] dark:text-[#EDEDEC] dark:hover:border-[#3E3E3A]">
                    登入
                    </Link>
                    <Link :href="route('register')"
                        class="inline-block rounded-sm border border-[#19140035] px-5 py-1.5 text-sm leading-normal text-[#1b1b18] hover:border-[#1915014a] dark:border-[#3E3E3A] dark:text-[#EDEDEC] dark:hover:border-[#62605b]">
                    註冊
                    </Link>
                </template>
            </nav>
        </header>
        <div
            class="duration-750 starting:opacity-0 flex w-full items-center justify-center opacity-100 transition-opacity lg:grow">
            <main class="flex  w-full max-w-[750px] flex-wrap content-start overflow-hidden rounded-lg lg:max-w-4xl lg:flex-row">
                <div class="w-full flex justify-content-center items-center p-4 bg-white rounded">
                    <label for="">工作事項</label>
                    <input class="border border-gray-500 p-1 mx-2" type="text" name="event" id="event" v-model="event">
                    <button class="border bg-red-200 px-2 py-2 rounded-2xl" @click="addEvent">
                        新增</button>
                </div>
                <h3 class="text-center w-full text-2xl">待辦事項清單</h3>
                <div id="lists" class="w-full">
                    <p v-for="event,idx in events" :key="idx" class="flex justify-between w-full" >
                        <div>

                            {{ idx+1 }}.{{ event }}
                        </div>
                        <div>
                            <button class="btn btn-yellow">編輯</button>
                            <button class="btn btn-red" @click="del(idx)">刪除</button>
                        </div>
                    </p>
                </div>
            </main>
        </div>
        <div class="h-14.5 hidden lg:block"></div>
    </div>
</template>
<style scoped>
.btn{
    @apply border px-4 py-1 rounded-2xl drop-shadow-lg
}
.btn-lime{
    @apply bg-lime-200 text-lime-800
}
.btn-yellow{
    @apply bg-yellow-800 text-yellow-100
}
.btn-red{
    @apply bg-red-200 text-red-800
}
</style>