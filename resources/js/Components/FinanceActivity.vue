<template>
    <!-- Recent activity -->
    <h2 class="mt-8 text-lg leading-6 font-medium text-gray-900">Recent activity</h2>
    <div class="flex flex-col mt-2">
        <div class="align-middle min-w-full overflow-x-auto shadow overflow-hidden sm:rounded-lg">
            <table class="min-w-full divide-y divide-gray-200">
                <thead>
                <tr>
                    <th class="px-6 py-3 bg-gray-50 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Transaction
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Amount
                    </th>
                    <th class="hidden px-6 py-3 bg-gray-50 text-left text-xs font-medium text-gray-500 uppercase tracking-wider md:block">
                        Status
                    </th>
                    <th class="px-6 py-3 bg-gray-50 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                        Date
                    </th>
                </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="transaction in transactions" :key="transaction.id" class="bg-white">
                    <td class="max-w-0 w-full px-6 py-4 whitespace-nowrap text-sm text-gray-900">
                        <div class="flex">
                            <a :href="transaction.href"
                               class="group inline-flex space-x-2 truncate text-sm">
                                <CashIcon
                                    class="flex-shrink-0 h-5 w-5 text-gray-400 group-hover:text-gray-500"
                                    aria-hidden="true"/>
                                <p class="text-gray-500 truncate group-hover:text-gray-900">
                                    {{ transaction.name }}
                                </p>
                            </a>
                        </div>
                    </td>
                    <td class="px-6 py-4 text-right whitespace-nowrap text-sm text-gray-500">
                        <span class="text-gray-900 font-medium">{{ transaction.amount }} </span>
                        {{ transaction.currency }}
                    </td>
                    <td class="hidden px-6 py-4 whitespace-nowrap text-sm text-gray-500 md:block">
                               <span
                                   :class="[statusStyles[transaction.status], 'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium capitalize']">
                               {{ transaction.status }}
                               </span>
                    </td>
                    <td class="px-6 py-4 text-right whitespace-nowrap text-sm text-gray-500">
                        <time :datetime="transaction.datetime">{{ transaction.date }}</time>
                    </td>
                </tr>
                </tbody>
            </table>
            <!-- Pagination -->
            <nav
                class="bg-white px-4 py-3 flex items-center justify-between border-t border-gray-200 sm:px-6"
                aria-label="Pagination">
                <div class="hidden sm:block">
                    <p class="text-sm text-gray-700">
                        Showing
                        {{ ' ' }}
                        <span class="font-medium">1</span>
                        {{ ' ' }}
                        to
                        {{ ' ' }}
                        <span class="font-medium">10</span>
                        {{ ' ' }}
                        of
                        {{ ' ' }}
                        <span class="font-medium">20</span>
                        {{ ' ' }}
                        results
                    </p>
                </div>
                <div class="flex-1 flex justify-between sm:justify-end">
                    <a href="#"
                       class="relative inline-flex items-center px-4 py-2 border border-gray-300 text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50">
                        Previous </a>
                    <a href="#"
                       class="ml-3 relative inline-flex items-center px-4 py-2 border border-gray-300 text-sm font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50">
                        Next </a>
                </div>
            </nav>
        </div>
    </div>
</template>

<script>
import { CashIcon } from '@heroicons/vue/solid'

const transactions = [
    {
        id: 1,
        name: 'Payment to Molly Sanders',
        href: '#',
        amount: '$20,000',
        currency: 'USD',
        status: 'success',
        date: 'July 11, 2020',
        datetime: '2020-07-11',
    },
    {
        id: 2,
        name: 'Payment to Doug Mann',
        href: '#',
        amount: '$19,5000',
        currency: 'USD',
        status: 'processing',
        date: 'July 14, 2020',
        datetime: '2020-07-11',
    },
    {
        id: 3,
        name: 'Payment to Erica Frost',
        href: '#',
        amount: '$8,750',
        currency: 'USD',
        status: 'success',
        date: 'July 1, 2020',
        datetime: '2020-07-11',
    },
    {
        id: 4,
        name: 'Payment to Miley Davis',
        href: '#',
        amount: '$2,000',
        currency: 'USD',
        status: 'success',
        date: 'June 17, 2020',
        datetime: '2020-07-11',
    },
    {
        id: 5,
        name: 'Payment to Molly Sanders',
        href: '#',
        amount: '$16,200',
        currency: 'USD',
        status: 'failed',
        date: 'June 10, 2020',
        datetime: '2020-07-11',
    },
    {
        id: 6,
        name: 'Payment to Miley Davis',
        href: '#',
        amount: '$10,300',
        currency: 'USD',
        status: 'success',
        date: 'June 9, 2020',
        datetime: '2020-07-11',
    },
]
const statusStyles = {
    success: 'bg-green-100 text-green-800',
    processing: 'bg-yellow-100 text-yellow-800',
    failed: 'bg-gray-100 text-gray-800',
}

export default {
    components: {
        CashIcon,
    },
    setup() {
        return {
            transactions,
            statusStyles,
        }
    },
}
</script>
