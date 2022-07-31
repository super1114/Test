<template>
    <div class="flex flex-col gap-14">
        <div class="flex items-center justify-center cursor-pointer" v-for="menu in menus" :key="menu.label" @click="changeMenu(menu.id)">
            <i :class="[menu.icon, ' text-lg transition', menu.id === currentMenu ? 'text-blue-600' : '']" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    data() {
        return {
            menus: [
                {
                    id: 0,
                    label: 'Home',
                    url: '/home',
                    icon: 'fa-regular fa-home'
                },
                {
                    id: 1,
                    label: 'Pie Chart',
                    url: '/pie-chart',
                    icon: 'fa-regular fa-chart-pie-simple'
                },
                {
                    id: 2,
                    label: 'Line Chart',
                    url: '/line-chart',
                    icon: 'fa-regular fa-chart-line-up'
                },
                {
                    id: 3,
                    label: 'Book',
                    url: '/book',
                    icon: 'fa-regular fa-book-blank'
                },
                {
                    id: 4,
                    label: 'More',
                    url: '/more',
                    icon: 'fa-regular fa-ellipsis-vertical'
                }
            ],
            currentMenu: 0
        }
    },
    methods: {
        changeMenu(menu: number) {
            this.currentMenu = menu;
        }
    }
})
</script>