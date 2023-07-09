<script setup>
import { ref, onMounted } from 'vue';
import { RouterLink, RouterView } from 'vue-router';
import MenuItem from "@/components/MenuItem.vue";
import MusicPlayer from './components/MusicPlayer.vue';

import ChevronLeft from "vue-material-design-icons/ChevronLeft.vue";
import ChevronRight from "vue-material-design-icons/ChevronRight.vue";
import ChevronDown from "vue-material-design-icons/ChevronDown.vue";
import ChevronUp from "vue-material-design-icons/ChevronUp.vue";

import { useSongStore } from '../src/stores/song'
import { storeToRefs } from 'pinia'
const useSong = useSongStore()
const { isPlaying, currentTrack } = storeToRefs(useSong)

onMounted(() => {
   isPlaying.value = false
})

let openMenu = ref(false)
</script>

<template>
    <div>
        <div
            class="w-[calc(100%-240px)] h-[60px] fixed right-0 z-20 bg-[#101010] bg-opacity-80 flex items-center justify-between">

            <div class="flex items-center ml-6">
                <button class="rounded-full bg-black p-[1px] cursor-pointer">
                    <ChevronLeft fillColor="#fff" :size="30" />
                </button>
                <button class="rounded-full bg-black p-[1px] ml-4 cursor-pointer">
                    <ChevronRight fillColor="#fff" :size="30" />
                </button>
            </div>
            <button @click="openMenu = !openMenu" :class="openMenu ? 'bg-[#282828]' : 'bg-black'"
                class="bg-black hover:bg-[#282828] rounded-full p-0.5 mr-8 mt-0.5 cursor-pointer">
                <div class="flex items-center">
                    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTt0t3DuB4KxJYutwU5JKB4Z_40P9be6ae89aFpOie9rA&s"
                        class="rounded-full" width="27">
                    <div class="text-white text-[14px] ml-1.5 font-semibold">Alex Ruso</div>
                    <ChevronDown v-if="!openMenu" fillColor="#fff" :size="25" />
                    <ChevronUp v-else fillColor="#fff" :size="25" />
                </div>
            </button>
            <span v-if="openMenu"
                class="fixed w-[190px] bg-[#282828] shadow-2xl z-50 rounded-sm top-[52px] right-[35px] p-1">
                <ul class="text-gray-200 font-semibold text-[14px]">
                    <li class="px-3 py-2.5 hover:bg-[#3E3030] border-b border-b-gray-600">Profile</li>
                    <li class="px-3 py-2.5 hover:bg-[#3E3030]">Logout</li>
                </ul>
            </span>
        </div>
        <div id="SideNav" class="h-[100%] p-6 w-[240px] fixed z-50 bg-black">
            <RouterLink to="/">
                <img src="/images/icons/spotify-logo.png" alt="">
            </RouterLink>
            <div class="my-8"></div>
            <ul>
                <RouterLink to="/">
                    <MenuItem class="ml-[1px]" :iconSize="23" name="Home" iconString="home" pageUrl="/" />
                </RouterLink>
                <RouterLink to="/search">
                    <MenuItem class="ml-[1px]" :iconSize="24" name="Search" iconString="search" pageUrl="/search">
                    </MenuItem>
                </RouterLink>
                <RouterLink to="/library">
                    <MenuItem class="ml-[2px]" :iconSize="23" name="Library" iconString="library" pageUrl="/library">
                    </MenuItem>
                </RouterLink>
                <div class="py-3 5"></div>
                <MenuItem :iconSize="24" name="Create Playlist" iconString="playlist" pageUrl="/playlist">
                </MenuItem>
                <MenuItem class="-ml-[1px]" :iconSize="27" name="Liked Songs" iconString="liked" pageUrl="/liked">
                </MenuItem>
            </ul>
            <div class="border-b border-b-gray-700"></div>
            <ul>
                <li class="font-semibold text-[13px] mt-3 text-gray-300 hover:text-white">My Playlist #1</li>
                <li class="font-semibold text-[13px] mt-3 text-gray-300 hover:text-white">My Playlist #2</li>
                <li class="font-semibold text-[13px] mt-3 text-gray-300 hover:text-white">My Playlist #3</li>
                <li class="font-semibold text-[13px] mt-3 text-gray-300 hover:text-white">My Playlist #4</li>
            </ul>
        </div>
    </div>
    <div class="fixed right-0 top-0 w-[calc(100%-240px)] overflow-auto h-full bg-gradient-to-b from-[#1c1c1c] to-black">
        <div class="mt-[70px]"></div>
        <RouterView />
        <div class="mb-[100px]"></div>
    </div>
    <MusicPlayer v-if="currentTrack" />
</template>