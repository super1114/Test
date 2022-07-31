<template>
    <div class="relative min-w-[992px] min-h-[100vh] bg-gray-100">
        <nav-bar>
            <template #left>
                <nav-bar-left-wrapper>
                    <button-circle><i class="fa-regular fa-arrow-left" /></button-circle>
                    <text-base font-weight="font-medium" font-size="text-lg">Assets</text-base>
                </nav-bar-left-wrapper>
            </template>

            <template #right>
                <nav-bar-right-wrapper>
                    <div class="flex flex-row border-r pr-5 gap-3">
                        <button-primary :active="page === 0" @click="changePage(0)">
                            <text-base font-weight="font-medium">Buy / Sell</text-base>
                        </button-primary>
                        <button-primary :active="page === 1" @click="changePage(1)">
                            <text-base font-weight="font-medium">Send / Receive</text-base>
                        </button-primary>
                        <button-circle>
                            <i class="fa-regular fa-bell" />
                        </button-circle>
                        <button-circle>
                            <i class="fa-solid fa-grid" />
                        </button-circle>
                    </div>
                    <avatar-base />
                </nav-bar-right-wrapper>
            </template>
        </nav-bar>
        <side-bar>
            <app-logo />
            <side-bar-menu />
        </side-bar>
        <slot />
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import NavBar from './NavBar.vue'
import SideBar from './SideBar.vue'
import AppLogo from '@/components/Layout/AppLogo.vue'
import TextBase from '@/components/Base/Text/TextBase.vue'
import NavBarLeftWrapper from '../components/Layout/NavBarLeftWrapper.vue'
import NavBarRightWrapper from '@/components/Layout/NavBarRightWrapper.vue'
import SideBarMenu from '@/components/Layout/SideBarMenu.vue'
import ButtonCircle from '../components/Base/Button/ButtonCircle.vue'
import ButtonPrimary from '@/components/Base/Button/ButtonPrimary.vue'
import AvatarBase from '@/components/Base/Avatar/AvatarBase.vue'

export default defineComponent({
    data() {
        return {
            page: 0
        }
    },
    methods: {
        changePage(page: number) {
            this.page = page;
        }
    },
    components: {
        NavBar,
        SideBar,
        AppLogo,
        NavBarLeftWrapper,
        NavBarRightWrapper,
        SideBarMenu,
        ButtonCircle,
        ButtonPrimary,
        TextBase,
        AvatarBase
    }
})
</script>