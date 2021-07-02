<template>
    <div>
       <el-container>
           <el-header height="auto">
               <el-row align="middle" class="pt-2"><el-col :span="3">
        <!-- BEGIN: Logo -->
        <inertia-link :href="route('dashboard')">
          <svg class="h-7" xmlns="http://www.w3.org/2000/svg" title="Packbee Logo" viewBox="0 0 1880 470"><path class="packbee-logo-color-1" d="M400 235L221 131c-8-5-19-5-28 0L14 235c-8 5-14 14-14 24v79c0 10 6 20 14 25l179 103c9 5 20 5 28 0l179-103c9-5 14-15 14-25v-79c0-10-5-19-14-24zM134 358l65-37c5-3 11-3 16 0l65 37c3 2 3 6 0 8l-65 37c-5 3-11 3-16 0l-65-37c-2-1-2-6 0-8zm223-74v35l-2 4-9 5h-4l-120-69c-9-5-20-5-29 0L73 328h-4l-10-5-2-4v-36c0-4 3-9 7-11l136-79a14 14 0 0114 0l137 79c4 2 6 7 6 12zM29 160c5 0 9-1 14-4l156-90c5-3 11-3 16 0l157 90c14 9 34 2 40-14 5-13 0-28-12-35L221 4c-8-5-19-5-28 0L15 107c-25 14-15 53 14 53 5 0-13 0 0 0 5 0-13 0 0 0zm495-31h94c19 0 37 3 52 16 15 12 21 31 21 50 0 18-6 38-20 50a80 80 0 01-53 16h-57v82h-37V129zm37 101h55l13-1 12-6c4-3 7-7 9-11 2-5 3-10 3-17s-1-13-3-18c-2-4-4-8-8-11l-11-5-15-2h-55v71zm198-101h40l82 214h-40l-20-57h-86l-20 57h-39l83-214zm-13 129h65l-32-92h-1l-32 92zm300-61c-6-25-24-42-50-43-28-1-50 14-60 39-20 47-5 125 57 125 32 0 51-26 54-56h37c-3 41-30 76-71 84-40 8-80-7-103-40-23-34-26-81-11-119 15-37 50-62 91-63 45-1 89 25 94 73h-38zm72-68h38v97l95-97h46l-85 85 91 129h-47l-70-102-30 30v72h-38V129zm206 0h104c24 0 52 8 61 34 8 26-3 54-28 65 32 7 46 41 38 72-9 34-46 43-77 43h-98V129zm37 90h61c18 0 32-12 32-30 0-20-13-29-32-29h-61v59zm0 94h66c21 0 36-13 36-34 0-22-15-33-36-33h-66v67zm174-184h154v32h-117v56h108v31h-108v63h119v32h-156V129zm189 0h154v32h-117v56h108v31h-108v63h119v32h-156V129z"/></svg>
        </inertia-link>
        <!-- END: Logo -->
        </el-col>
        <el-col :span="18" class="-mt-2">
            <el-row align="middle" justify="center">
                <el-col class="menu-item mt-2" :span="6" :class="{'active': route().current() === 'dashboard'}">
                    <inertia-link :href="route('dashboard')" >
                        Dashboard
                    </inertia-link>
                </el-col>
                <el-col class="menu-item mt-2" :span="6" :class="{'active': route().current() === 'inventory'}">
                    <inertia-link :href="route('inventory')" >
                        Lagerbestand
                    </inertia-link>
                </el-col>
                <el-col class="menu-item mt-2" :span="6" :class="{'active': route().current() === 'shipping'}">
                    <inertia-link :href="route('shipping')" >
                        Versand
                    </inertia-link>
                </el-col>
                <el-col class="menu-item mt-2" :span="6" :class="{'active': route().current() === 'barcode'}">
                    <inertia-link :href="route('barcode')" >
                        Barcode
                    </inertia-link>
                </el-col>
            </el-row>
        </el-col>
        <el-col :span="3" class="text-right">
        <!-- BEGIN: Account Menu -->
        <el-dropdown>
            <div class="el-dropdown-link"><span class="w-10 h-10 -mt-1 rounded-full overflow-hidden shadow-lg  image-fit zoom-in scale-110">
                <img class="profile-image h-10 w-10 -mt-1 rounded-full object-cover" :src="$page.props.user.profile_photo_url" :alt="$page.props.user.name" />
            </span></div>
            <template #dropdown>
                <el-dropdown-menu>
                    <div class="p-4">
                            <div class="text-sm font-medium">{{ $page.props.user.name }}</div>
                            <div class="text-xs text-theme-41 mt-0.5 dark:text-gray-600">
                            {{ $page.props.user.current_team.name }}
                            </div>
                    </div>
                    <el-dropdown-item>
                        <inertia-link :href="route('teams.show', $page.props.user.current_team)">
                            Team Settings
                        </inertia-link>
                    </el-dropdown-item>
                    <el-dropdown-item>
                        <inertia-link :href="route('teams.create')" v-if="$page.props.jetstream.canCreateTeams">
                            Create New Team
                        </inertia-link>
                    </el-dropdown-item>
                    <el-dropdown-item divided>
                        <inertia-link :href="route('profile.show')">
                            Profile
                        </inertia-link>
                    </el-dropdown-item>
                    <el-dropdown-item>
                        <inertia-link :href="route('api-tokens.index')" v-if="$page.props.jetstream.hasApiFeatures">
                            API Tokens
                        </inertia-link>
                    </el-dropdown-item>
                <el-dropdown-item>
                    Reset Password
                </el-dropdown-item>
                <el-dropdown-item divided>
                    <inertia-link method="post" :href="route('logout')">
                        Log Out
                    </inertia-link>
                </el-dropdown-item>
                </el-dropdown-menu>
            </template>
        </el-dropdown>
        </el-col></el-row>
    </el-header>
    <el-main class="mx-4 mb-4">
        <slot></slot>
    </el-main>
    </el-container>
    </div>
</template>

<style lang="scss">
    @import "../../scss/element-plus/mixins/mixins";
    .packbee-logo-color-1{
        fill: $--color-white;
    }
    .el-header {
        background: $--color-primary-dark-4;
    }
    .profile-image{
        box-shadow: 0 1px 2px 0 $--color-white;
    }
    .menu-item{
        height: 50px;
        padding: 0 2rem;
        border-radius: 1rem 1rem 0 0;
        position:relative;
        display: flex;
        justify-content: center;
        align-items: center;
        width:100%;
        color: $--color-white;
    }
    .menu-item.active{
        background: $--background-color-base;
        color: $--color-primary-black;
    }
    .menu-item.active::before,
    .menu-item.active::after{
        position:absolute;
        bottom:-1rem;
        content: "";
        width: 3rem;
        height: 3rem;
        border-bottom-width: 1rem;
        border-color: $--background-color-base;
    }

    .menu-item.active::before{
        border-right-width: 1rem;
        border-bottom-right-radius: 2rem;
        left:-2rem
    }

    .menu-item.active::after{
        border-left-width: 1rem;
        border-bottom-left-radius: 2rem;
        right: -2rem;
    }
    .el-main{
        background: $--background-color-base;
        border-radius: 1rem;
    }
    body, html, .el-container{
        background: $--color-primary-dark-4;
    }
</style>
