<!-- This example requires Tailwind CSS v2.0+ -->
<template>
    <div>
        <h3 class="mt-8 text-lg leading-6 font-medium text-gray-900">Projects</h3>
        <ul role="list" class="mt-3 grid grid-cols-1 gap-5 sm:gap-6 sm:grid-cols-2 lg:grid-cols-4">
            <li v-for="project in projects" :key="project.name" class="col-span-1 flex shadow-sm rounded-md">
                <div :class="[project.bgColor, 'flex-shrink-0 flex items-center justify-center w-16 text-white text-sm font-medium rounded-l-md']">
                    {{ project.initials }}
                </div>
                <div class="flex-1 flex items-center justify-between border-t border-r border-b border-gray-200 bg-white rounded-r-md truncate">
                    <div class="flex-1 px-4 py-2 text-sm truncate">
                        <a :href="project.href" class="text-gray-900 font-medium hover:text-gray-600">{{ project.name }}</a>
                        <p class="text-gray-500">{{ project.members }} Members</p>
                    </div>
                    <div class="flex-shrink-0 pr-2">
                        <button type="button" class="w-8 h-8 bg-white inline-flex items-center justify-center text-gray-400 rounded-full bg-transparent hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                            <span class="sr-only">Open options</span>
                            <DotsVerticalIcon class="w-5 h-5" aria-hidden="true" />
                        </button>
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
import { DotsVerticalIcon } from '@heroicons/vue/solid'

const projects = [
    { name: 'Graph API', initials: 'GA', href: '#', members: 16, bgColor: 'bg-pink-600' },
    { name: 'Continuous Integration', initials: 'CI', href: '#', members: 12, bgColor: 'bg-purple-600' },
    { name: 'Stock Launch', initials: 'SL', href: '#', members: 16, bgColor: 'bg-yellow-500' },
    { name: 'Serverless Functions', initials: 'SF', href: '#', members: 8, bgColor: 'bg-green-500' },
]

export default {
    components: {
        DotsVerticalIcon,
    },
    setup() {
        return {
            projects,
        }
    },
}
</script>
