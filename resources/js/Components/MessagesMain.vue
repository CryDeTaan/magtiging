<template>
    <div class="max-w-3xl mx-auto sm:px-6 lg:max-w-7xl lg:px-8 lg:grid lg:grid-cols-10 lg:gap-8">
        <main class="lg:col-span-8 xl:col-span-6">
            <div class="px-4 sm:px-0">
                <div class="hidden sm:block">
                    <nav class="relative z-0 rounded-lg shadow flex divide-x divide-gray-200" aria-label="Tabs">
                        <a v-for="(tab, tabIdx) in tabs" :key="tab.name" :href="tab.href"
                           :aria-current="tab.current ? 'page' : undefined"
                           :class="[tab.current ? 'text-gray-900' : 'text-gray-500 hover:text-gray-700', tabIdx === 0 ? 'rounded-l-lg' : '', tabIdx === tabs.length - 1 ? 'rounded-r-lg' : '', 'group relative min-w-0 flex-1 overflow-hidden bg-white py-4 px-6 text-sm font-medium text-center hover:bg-gray-50 focus:z-10']">
                            <span>{{ tab.name }}</span>
                            <span aria-hidden="true"
                                  :class="[tab.current ? 'bg-indigo-500' : 'bg-transparent', 'absolute inset-x-0 bottom-0 h-0.5']"/>
                        </a>
                    </nav>
                </div>
            </div>
            <div class="mt-4">
                <h1 class="sr-only">Recent questions</h1>
                <ul role="list" class="space-y-4">
                    <li v-for="message in messages" :key="message.id"
                        class="bg-white px-4 py-6 border border-1 shadow sm:p-6 sm:rounded-lg">
                        <article :aria-labelledby="'question-title-' + message.id">
                            <div>
                                <div class="flex space-x-3">
                                    <div class="flex-shrink-0">
                                        <img class="h-10 w-10 rounded-full" :src="message.author.image_url + '?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80'" alt=""/>
                                    </div>
                                    <div class="min-w-0 flex-1">
                                        <p class="text-sm font-medium text-gray-900">
                                            <a href="#"
                                                class="hover:underline">{{ message.author.name }}
                                            </a>
                                            <span class="text-gray-500">&nbspsent a message to <span class="font-bold">{{ message.user.name }}</span> on:</span>
                                        </p>
                                        <p class="text-sm text-gray-500">
                                            <a href="#" class="hover:underline">
                                                <time :datetime="message.updated_at">{{ message.date_string }}</time>
                                            </a>
                                        </p>
                                    </div>
                                    <div class="flex-shrink-0 self-center flex">
                                        <Menu as="div" class="relative inline-block text-left">
                                            <div>
                                                <MenuButton
                                                    class="-m-2 p-2 rounded-full flex items-center text-gray-400 hover:text-gray-600">
                                                    <span class="sr-only">Open options</span>
                                                    <DotsVerticalIcon class="h-5 w-5" aria-hidden="true"/>
                                                </MenuButton>
                                            </div>

                                            <transition enter-active-class="transition ease-out duration-100"
                                                        enter-from-class="transform opacity-0 scale-95"
                                                        enter-to-class="transform opacity-100 scale-100"
                                                        leave-active-class="transition ease-in duration-75"
                                                        leave-from-class="transform opacity-100 scale-100"
                                                        leave-to-class="transform opacity-0 scale-95">
                                                <MenuItems
                                                    class="origin-top-right absolute right-0 mt-2 w-56 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
                                                    <div class="py-1">
                                                        <MenuItem v-slot="{ active }">
                                                            <a href="#"
                                                               :class="[active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'flex px-4 py-2 text-sm']">
                                                                <StarIcon class="mr-3 h-5 w-5 text-gray-400"
                                                                          aria-hidden="true"/>
                                                                <span>Add to favorites</span>
                                                            </a>
                                                        </MenuItem>
                                                        <MenuItem v-slot="{ active }">
                                                            <a href="#"
                                                               :class="[active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'flex px-4 py-2 text-sm']">
                                                                <CodeIcon class="mr-3 h-5 w-5 text-gray-400"
                                                                          aria-hidden="true"/>
                                                                <span>Embed</span>
                                                            </a>
                                                        </MenuItem>
                                                        <MenuItem v-slot="{ active }">
                                                            <a href="#"
                                                               :class="[active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'flex px-4 py-2 text-sm']">
                                                                <FlagIcon class="mr-3 h-5 w-5 text-gray-400"
                                                                          aria-hidden="true"/>
                                                                <span>Report content</span>
                                                            </a>
                                                        </MenuItem>
                                                    </div>
                                                </MenuItems>
                                            </transition>
                                        </Menu>
                                    </div>
                                </div>
                                <h2 :id="'question-title-' + message.id"
                                    class="mt-4 text-base font-medium text-gray-900">
                                    {{ message.title }}
                                </h2>
                            </div>
                            <div class="mt-2 text-sm text-gray-700 space-y-4" v-html="message.body"/>
                            <div class="mt-6 flex justify-between space-x-8">
                                <div class="flex space-x-6">
                                    <span class="inline-flex items-center text-sm">
                                        <button type="button"
                                                class="inline-flex space-x-2 text-gray-400 hover:text-gray-500">
                                          <ThumbUpIcon class="h-5 w-5" aria-hidden="true"/>
                                          <span class="font-medium text-gray-900">{{ message.likes }}</span>
                                          <span class="sr-only">likes</span>
                                        </button>
                                  </span>
                                    <span class="inline-flex items-center text-sm">
                                        <button type="button"
                                                class="inline-flex space-x-2 text-gray-400 hover:text-gray-500">
                                          <ChatAltIcon class="h-5 w-5" aria-hidden="true"/>
                                          <span class="font-medium text-gray-900">{{ message.replies }}</span>
                                          <span class="sr-only">replies</span>
                                        </button>
                                    </span>
                                    <span class="inline-flex items-center text-sm">
                                        <button type="button"
                                                class="inline-flex space-x-2 text-gray-400 hover:text-gray-500">
                                          <EyeIcon class="h-5 w-5" aria-hidden="true"/>
                                          <span class="font-medium text-gray-900">{{ message.views }}</span>
                                          <span class="sr-only">views</span>
                                        </button>
                                    </span>
                                </div>
                                <div class="flex text-sm">
                                  <span class="inline-flex items-center text-sm">
                                    <button type="button"
                                            class="inline-flex space-x-2 text-gray-400 hover:text-gray-500">
                                      <ShareIcon class="h-5 w-5" aria-hidden="true"/>
                                      <span class="font-medium text-gray-900">Share</span>
                                    </button>
                                  </span>
                                </div>
                            </div>
                        </article>
                    </li>
                </ul>
            </div>
        </main>
        <aside class="hidden xl:block xl:col-span-4">
            <div class="sticky top-4 space-y-4">
                <messages-to-follow/>
                <messages-trending/>
            </div>
        </aside>
    </div>

</template>

<script>
import {Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import {
    ChatAltIcon,
    CodeIcon,
    DotsVerticalIcon,
    EyeIcon,
    FlagIcon,
    ShareIcon,
    StarIcon,
    ThumbUpIcon,
} from '@heroicons/vue/solid'

import MessagesToFollow from "./MessagesToFollow";
import MessagesTrending from "./MessagesTrending";

const tabs = [
    {name: 'Recent', href: '#', current: true},
    {name: 'Most Liked', href: '#', current: false},
    {name: 'Most Answers', href: '#', current: false},
]

export default {
    components: {
        MessagesTrending,
        MessagesToFollow,
        Menu,
        MenuButton,
        MenuItem,
        MenuItems,
        ChatAltIcon,
        CodeIcon,
        DotsVerticalIcon,
        EyeIcon,
        FlagIcon,
        ShareIcon,
        StarIcon,
        ThumbUpIcon,
    },
    props: ['messages'],
    setup() {
        return {
            tabs,
        }
    },
}
</script>
