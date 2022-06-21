<template>
    <Head :title="timeShow" />
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
                    @click="switchTab(1)"
                    :class="
                        tab == 1
                            ? 'text-white font-bold bg-gray-900 px-3 py-1 cursor-pointer rounded-md bg-opacity-10'
                            : 'text-white font-semibold px-3 py-1 rounded-md cursor-pointer bg-opacity-10'
                    "
                >
                    Pomodoro
                </div>
                <div
                    @click="switchTab(2)"
                    :class="
                        tab == 2
                            ? 'text-white font-bold bg-gray-900 px-3 py-1 cursor-pointer rounded-md bg-opacity-10'
                            : 'text-white font-semibold px-3 py-1 rounded-md cursor-pointer bg-opacity-10'
                    "
                >
                    Short Break
                </div>
                <div
                    @click="switchTab(3)"
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
                {{ timeShow }}
            </div>

            <div class="text-center">
                <button
                    v-if="!timmerRunning"
                    class="bg-white mx-auto mt-4 rounded-t-md pt-3"
                >
                    <h1
                        class="font-bold px-16 pb-3 text-[22px] transition-all duration-500"
                        :class="
                            tab == 1
                                ? 'text-[#D95550]'
                                : tab == 2
                                ? 'text-[#4c9195]'
                                : 'text-[#457d9f]'
                        "
                        @click="startTimer()"
                    >
                        Start
                    </h1>
                    <div class="bg-gray-200 border-4 w-full"></div>
                </button>
                <button v-else class="bg-white mx-auto mt-4 rounded-t-md pt-3">
                    <h1
                        class="font-bold px-16 pb-3 text-[22px] transition-all duration-500"
                        :class="
                            tab == 1
                                ? 'text-[#D95550]'
                                : tab == 2
                                ? 'text-[#4c9195]'
                                : 'text-[#457d9f]'
                        "
                        @click="stopTimer()"
                    >
                        Stop
                    </h1>
                    <div class="bg-gray-200 border-4 w-full"></div>
                </button>
            </div>
        </div>
        <!-- Timer Box End -->

        <!-- Settings Section Start -->
        <div
            v-if="settingsShow"
            class="bg-gray-900 flex justify-center bg-opacity-40 p-8 fixed top-0 w-screen min-h-screen"
        >
            <div
                class="w-3/12 m-4 px-4 bg-white rounded-lg break-words p-4 h-auto inline-block"
            >
                <div class="flex justify-between">
                    <div
                        class="flex justify-end text-gray-600 text-lg font-bold m-2 cursor-pointer"
                    >
                        TIMER SETTING
                    </div>
                    <div
                        class="flex justify-end text-gray-600 text-lg font-bold m-2 cursor-pointer"
                        @click="settingsShow = !settingsShow"
                    >
                        X
                    </div>
                </div>
                <hr />

                <div class="p-4">
                    <h1 class="text-black font-semibold">Time (minutes)</h1>
                    <div class="grid grid-cols-3 gap-6">
                        <div>
                            <label
                                for=""
                                class="text-gray-400 font-semibold text-sm"
                                >Pomodoro</label
                            >
                            <input
                                type="number"
                                maxlength="5"
                                @change="pomodoroTimeChanged($event)"
                                class="flex w-full bg-gray-200 outline-none ring-0 border-0 rounded"
                                min="0"
                                :value="settings.pomodoro_time"
                                minlength="0"
                            />
                        </div>
                        <div>
                            <label
                                for=""
                                class="text-gray-400 font-semibold text-sm"
                                >Short Break</label
                            >
                            <input
                                type="number"
                                maxlength="5"
                                @change="shortBreakTimeChanged($event)"
                                class="flex w-full bg-gray-200 outline-none ring-0 border-0 rounded"
                                min="0"
                                :value="settings.short_break_time"
                                minlength="0"
                            />
                        </div>
                        <div>
                            <label
                                for=""
                                class="text-gray-400 font-semibold text-sm"
                                >Long Break</label
                            >
                            <input
                                type="number"
                                maxlength="5"
                                @change="longBreakTimeChanged($event)"
                                :value="settings.long_break_time"
                                class="flex w-full bg-gray-200 outline-none ring-0 border-0 rounded"
                                min="0"
                                minlength="0"
                            />
                        </div>
                    </div>
                </div>

                <hr />

                <div class="p-4 flex justify-between items-center">
                    <h1 class="text-black font-semibold">Auto start Breaks?</h1>
                    <input
                        type="checkbox"
                        v-model="settings.auto_start_breaks"
                        @change="autoStartBreaks($event)"
                    />
                </div>
                <hr />

                <div class="p-4 flex justify-between items-center">
                    <h1 class="text-black font-semibold">
                        Auto start Pomodoros?
                    </h1>
                    <input
                        type="checkbox"
                        v-model="settings.auto_start_pomodoros"
                        @change="autoStartPomodoros($event)"
                    />
                </div>
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
            settingsShow: true,
            tab: 1,
            time: 300,
            timeShow: "00:00",
            interval: null,
            timmerRunning: false,

            settings: {
                pomodoro_time: 0,
                short_break_time: 0,
                long_break_time: 0,
                auto_start_breaks: false,
                auto_start_pomodoros: false,
            },
        };
    },

    mounted() {
        this.time = localStorage.getItem("pomodoro_time_seconds") || 1500;
        this.settings.pomodoro_time = this.time / 60;

        this.settings.short_break_time =
            localStorage.getItem("short_break_time_seconds") || 300;

        this.settings.short_break_time = this.settings.short_break_time / 60;

        this.settings.long_break_time =
            localStorage.getItem("long_break_time_seconds") || 900;
        this.settings.long_break_time = this.settings.long_break_time / 60;

        this.settings.auto_start_breaks =
            localStorage.getItem("auto_start_breaks") || false;
        this.settings.auto_start_pomodoros =
            localStorage.getItem("auto_start_pomodoros") || false;
        this.updateTime();
    },

    methods: {
        startTimer() {
            this.timmerRunning = true;

            this.interval = setInterval(() => {
                this.updateTime();
            }, 1000);
        },
        stopTimer() {
            clearInterval(this.interval);
            this.timmerRunning = false;
        },
        updateTime() {
            if (this.time < 0) {
                clearInterval(this.interval);
                this.timmerRunning = false;

                if (this.tab == 1) {
                    this.tab = 2;
                    this.timeValuesUpdate();

                    if (this.settings.auto_start_breaks) {
                        this.startTimer();
                    }
                    return;
                } else {
                    this.tab = 1;

                    if (this.settings.auto_start_pomodoros) {
                        this.startTimer();
                    }
                    this.timeValuesUpdate();

                    return;
                }
            }
            var minutes = this.time / 60;
            var seconds = this.time % 60;

            minutes = Math.floor(minutes);
            seconds = Math.floor(seconds);

            if (minutes < 10) {
                minutes = "0" + minutes;
            }
            if (seconds < 10) {
                seconds = "0" + seconds;
            }

            this.timeShow = "" + minutes + ":" + seconds;
            this.time--;
        },

        switchTab(tab) {
            if (this.timmerRunning) {
                if (confirm("Timer is still running do you want to continue")) {
                    clearInterval(this.interval);
                    this.timmerRunning = false;

                    this.tab = tab;
                    this.timeValuesUpdate();
                }
            } else {
                this.tab = tab;
                this.timeValuesUpdate();
            }
        },

        timeValuesUpdate() {
            if (this.tab == 1) {
                this.time =
                    localStorage.getItem("pomodoro_time_seconds") || 1500;
            }
            if (this.tab == 2) {
                this.time =
                    localStorage.getItem("short_break_time_seconds") || 300;
            }
            if (this.tab == 3) {
                this.time =
                    localStorage.getItem("long_break_time_seconds") || 900;
            }

            this.updateTime();
        },

        pomodoroTimeChanged(event) {
            localStorage.setItem(
                "pomodoro_time_seconds",
                event.target.value * 60
            );
            this.time = event.target.value * 60;
            this.settings.pomodoro_time = this.time / 60;

            this.updateTime();
        },

        shortBreakTimeChanged(event) {
            localStorage.setItem(
                "short_break_time_seconds",
                event.target.value * 60
            );

            this.time = event.target.value * 60;
            this.settings.short_break_time = this.time / 60;
            this.updateTime();
        },

        longBreakTimeChanged(event) {
            localStorage.setItem(
                "long_break_time_seconds",
                event.target.value * 60
            );

            this.time = event.target.value * 60;
            this.settings.long_break_time = this.time / 60;
            this.updateTime();
        },

        autoStartBreaks(event) {
            localStorage.setItem(
                "auto_start_breaks",
                this.settings.auto_start_breaks
            );
        },
        autoStartPomodoros(event) {
            localStorage.setItem(
                "auto_start_pomodoros",
                this.settings.auto_start_pomodoros
            );
        },
    },
};
</script>

<style>
/* 'ArialRounded', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, Helvetica, Arial, sans-serif,
    'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol' */
</style>
