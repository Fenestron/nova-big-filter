<template>
    <div v-if="filters.length > 0" class="bg-30 border-b border-60">
        <scroll-wrap :height="card.filterMaxHeight ? card.filterMaxHeight : 350">
            <div v-if="! card.filterHideTitle" class="py-2 w-full block text-xs uppercase tracking-wide text-center text-80 dim font-bold focus:outline-none">
                {{this.card.filterMenuTitle ? this.card.filterMenuTitle : 'Filter Menu'}}
            </div>
            <!--<div v-if="filtersAreApplied" class="bg-30 border-b border-60">-->
            <!--<button-->
            <!--@click="$emit('clear-selected-filters')"-->
            <!--class="py-2 w-full block text-xs uppercase tracking-wide text-center text-80 dim font-bold focus:outline-none"-->
            <!--&gt;-->
            <!--{{ __('Reset Filters') }}-->
            <!--</button>-->
            <!--</div>-->

            <!-- Custom Filters -->
            <div v-for="filters in this.filterRows" style="display: flex; justify-content: space-between; width: 100%">
                <div v-for="(filter, index) in filters" style="width: 100%">
                    <component
                            v-if="filter"
                            :resource-name="resourceName"
                            :key="filter.name"
                            :filter-key="filter.class"
                            :is="filter.component"
                            @input="$emit('filter-changed')"
                            @change="$emit('filter-changed')"
                    />
                </div>
            </div>

            <!-- Soft Deletes -->
            <div v-if="softDeletes && showTrashedOption">
                <h3 slot="default" class="text-sm uppercase tracking-wide text-80 bg-30 p-3">
                    {{ __('Trashed') }}
                </h3>

                <div class="p-2">
                    <select
                            slot="select"
                            class="block w-full form-control-sm form-select"
                            dusk="trashed-select"
                            :value="trashed"
                            @change="trashedChanged"
                    >
                        <option value="" selected>&mdash;</option>
                        <option value="with">{{ __('With Trashed') }}</option>
                        <option value="only">{{ __('Only Trashed') }}</option>
                    </select>
                </div>
            </div>
        </scroll-wrap>
    </div>
</template>

<script>
    export default {
        props: {
            card: {
                filterMenuTitle: String,
                filterMaxHeight: Number,
                filterHideTitle: {
                    type: Boolean,
                    default: false
                }
            },
            resourceName: String,
            softDeletes: Boolean,
            viaResource: String,
            viaHasOne: Boolean,
            trashed: {
                type: String,
                validator: value => ['', 'with', 'only'].indexOf(value) != -1,
            },
            perPage: [String, Number],
            showTrashedOption: {
                type: Boolean,
                default: true,
            },
        },
        methods: {
            trashedChanged(event) {
                this.$emit('trashed-changed', event.target.value)
            },

            perPageChanged(event) {
                this.$emit('per-page-changed', event.target.value)
            }
        },

        computed: {
            /**
             * Return the filters from state
             */
            filters() {
                return this.$store.getters[`${this.resourceName}/filters`]
            },

            /**
             * Determine via state whether filters are applied
             */
            filtersAreApplied() {
                return this.$store.getters[`${this.resourceName}/filtersAreApplied`]
            },

            /**
             * Return the number of active filters
             */
            activeFilterCount() {
                return this.$store.getters[`${this.resourceName}/activeFilterCount`]
            },

            filterRows(){
                return _.chunk(this.filters, this.filters.length)
            }
        },
    }
</script>
