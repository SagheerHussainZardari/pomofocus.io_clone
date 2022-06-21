<template>
    <Head title="00:00" />
    <div
        class="w-screen h-screen transition-all duration-500"
        :class="
            tab == 1
                ? 'bg-[#D95550]'
                : tab == 2
                ? 'bg-[#4c9195]'
                : 'bg-[#457d9f]'
        "
    >
        <!-- Header Start -->
        <div class="w-4/12 mx-auto py-4">
            <div class="flex justify-between">
                <a href="/" class="flex items-center text-white">Pomofocus</a>

                <div
                    @click="settingsShow = !settingsShow"
                    class="bg-white bg-opacity-30 text-sm text-gray-300 hover:text-white px-3 py-2 cursor-pointer rounded"
                >
                    Setting
                </div>
            </div>
            <div
                class="border-[1px] border-opacity-20 border-gray-600 my-2"
            ></div>
        </div>
        <!-- Header End -->

        <!-- Timer Box Start -->
        <div class="bg-white bg-opacity-10 rounded-md p-6 w-3/12 mx-auto mt-6">
            <div class="flex justify-center gap-2 w-10/12 mx-auto">
                <div
                    @click="tab = 1"
                    :class="
                        tab == 1
                            ? 'text-white font-bold bg-gray-900 px-3 py-1 cursor-pointer rounded-md bg-opacity-10'
                            : 'text-white font-semibold px-3 py-1 rounded-md cursor-pointer bg-opacity-10'
                    "
                >
                    Pomodoro
                </div>
                <div
                    @click="tab = 2"
                    :class="
                        tab == 2
                            ? 'text-white font-bold bg-gray-900 px-3 py-1 cursor-pointer rounded-md bg-opacity-10'
                            : 'text-white font-semibold px-3 py-1 rounded-md cursor-pointer bg-opacity-10'
                    "
                >
                    Short Break
                </div>
                <div
                    @click="tab = 3"
                    :class="
                        tab == 3
                            ? 'text-white font-bold bg-gray-900 px-3 py-1 cursor-pointer rounded-md bg-opacity-10'
                            : 'text-white font-semibold px-3 py-1 rounded-md cursor-pointer bg-opacity-10'
                    "
                >
                    Long Break
                </div>
            </div>

            <div class="mt-4 text-white text-[120px] text-center font-bold">
                00:59
            </div>

            <div class="text-center">
                <button class="bg-white mx-auto mt-4 rounded-t-md pt-3">
                    <h1
                        class="font-bold px-16 pb-3 text-[22px] transition-all duration-500"
                        :class="
                            tab == 1
                                ? 'text-[#D95550]'
                                : tab == 2
                                ? 'text-[#4c9195]'
                                : 'text-[#457d9f]'
                        "
                    >
                        Start
                    </h1>
                    <div class="bg-gray-200 border-4 w-full"></div>
                </button>
            </div>
        </div>
        <!-- Timer Box End -->

        <!-- Settings Section Start -->
        <div
            v-if="settingsShow"
            class="bg-gray-900 flex justify-center bg-opacity-40 p-12 fixed top-0 w-screen min-h-screen"
        >
            <div
                class="w-3/12 m-6 px-4 bg-white rounded-lg break-words h-auto inline-block"
            >
                <div
                    class="flex justify-end text-gray-700 text-lg font-bold m-4 cursor-pointer"
                    @click="settingsShow = !settingsShow"
                >
                    X
                </div>
                Settings
                SettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettingsSettings
            </div>
        </div>
        <!-- Settings Section End -->
    </div>
</template>

<script>
import { Head } from "@inertiajs/inertia-vue3";

export default {
    components: {
        Head,
    },

    data() {
        return {
            settingsShow: false,
            tab: 1,
        };
    },
};
</script>

<style>
/* 'ArialRounded', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, Helvetica, Arial, sans-serif,
    'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol' */
</style>
