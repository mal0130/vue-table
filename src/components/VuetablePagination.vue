<template>
        <div class="{{wrapperClass}}">
            <a @click="loadPage(1)"
                class="btn-nav {{linkClass}} {{isOnFirstPage ? disabledClass : ''}}">
                    <i v-if="icons.first != ''" class="{{icons.first}}"></i>
                    <span v-else>&laquo;</span>
            </a>
            <a @click="loadPage('prev')"
                class="btn-nav {{linkClass}} {{isOnFirstPage ? disabledClass : ''}}">
                    <i v-if="icons.next != ''" class="{{icons.prev}}"></i>
                    <span v-else>&nbsp;&lsaquo;</span>
            </a>
            <template v-if="notEnoughPages">
                <template v-for="n in totalPage">
                    <a @click="loadPage(n+1)"
                        class="{{pageClass}} {{isCurrentPage(n+1) ? activeClass : ''}}">
                            {{ n+1 }}
                    </a>
                </template>
            </template>
            <template v-else>
               <template v-for="n in windowSize">
                   <a @click="loadPage(windowStart+n)"
                        class="{{pageClass}} {{isCurrentPage(windowStart+n) ? activeClass : ''}}">
                        {{ windowStart+n }}
                   </a>
               </template>
            </template>
            <a @click="loadPage('next')"
                class="btn-nav {{linkClass}} {{isOnLastPage ? disabledClass : ''}}">
                <i v-if="icons.next != ''" class="{{icons.next}}"></i>
                <span v-else>&rsaquo;&nbsp;</span>
            </a>
            <a @click="loadPage(totalPage)"
                class="btn-nav {{linkClass}} {{isOnLastPage ? disabledClass : ''}}">
                <i v-if="icons.last != ''" class="{{icons.last}}"></i>
                <span v-else>&raquo;</span>
            </a>
            <span>{{tablePagination.current_page}} / {{totalPage}}</span>
            <div class="vuetable-pagination-jump">
                <span>到第</span>
                <input class="form-control" type="text" v-model="jumpPage" @keyup.enter="loadPage(jumpPage)">
                <span>页</span>
                <a @click="loadPage(jumpPage)" class="btn btn-default">
                    <span>确认</span>
                </a>
            </div>
        </div>
</template>

<script>
import PaginationMixin from './VuetablePaginationMixin.vue'

export default {
    mixins: [PaginationMixin],
}
</script>