<template>
    <div class="home">
        <div class="container">
            <div class="row">
                <div class="col-sm-4 offset-sm-2 col-md-6 offset-md-0">
                    <draggable
                        class="list-group"
                        ghostClass="sortable-placeholder"
                        animation="250"
                        :list="arr"
                        group="people"
                        @start="fnStart"
                        @end="fnEnd"
                        @update="fnUpdate"
                        @change="fnChange"
                    >
                        <div
                            class="list-group-item"
                            v-for="item in arr"
                            :key="item.id"
                        >{{item.name}}</div>
                    </draggable>
                </div>
                <div class="col-sm-4 col-md-6 text-left">
                    <h4>List</h4>
                    <pre>
                        {{arr}}
                    </pre>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
// 支持事件: start, add, remove, update, end, choose, unchoose, sort, filter, clone
import draggable from "vuedraggable";
export default {
    name: "Home",
    components: {
        draggable
    },
    data() {
        return {
            arr: [
                { id: 1, name: "aaa" },
                { id: 2, name: "bbb" },
                { id: 3, name: "ccc" },
                { id: 4, name: "ddd" }
            ]
        };
    },
    methods: {
        fnStart(evt) {
            // Element dragging started
            // console.log(evt);
            console.log("Start", evt.oldIndex);
        },
        fnEnd(evt) {
            // Element dragging ended
            console.log("end", evt.oldIndex, evt.newIndex);
            var itemEl = evt.item; // dragged HTMLElement
            evt.to; // target list
            evt.from; // previous list
            evt.oldIndex; // element's old index within old parent
            evt.newIndex; // element's new index within new parent
            evt.oldDraggableIndex; // element's old index within old parent, only counting draggable elements
            evt.newDraggableIndex; // element's new index within new parent, only counting draggable elements
            evt.clone; // the clone element
            evt.pullMode; // when item is in another sortable: `"clone"` if cloning, `true` if moving
        },
        fnUpdate(evt) {
            // Changed sorting within list
            console.log("pdate", evt.oldIndex, evt.newIndex);
        },
        fnChange(evt) {
            console.log("change", evt);
        }
    }
};
</script>
<style scoped>
.list-group {
    height: 100%;
    background-color: #fcc;
}
.sortable-placeholder {
    border: 2px dashed #2878f0;
}
</style>
