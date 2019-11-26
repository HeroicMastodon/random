<template>
    <div class="wrapper">
        <div v-for="(i, index) in 24" :key="index" class="time-box"></div>
        <div
            :id="id"
            :class="'box' + myClass"
            :style="{top}"
            @mousedown.self="mouseDown"
        >
            Some text
        </div>
        <div 
            v-for="(item) in items" :key="item.id"
            :id="item.id"
            :class="'box' + myClass"
            :style="{top: item.time}"
            @mousedown.self="mouseDown"
        >
            {{item.name}}
        </div>
    </div>

    <!-- 
    <div class="v-calendar-daily__day v-future">
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-calendar-daily__day-interval" style="height: 40px;"></div>
        <div class="v-event-timed-container">
            <div
                class="v-event-timed secondary white--text"
                style="top: 500px; height: 120px; left: 0%; right: 0%;"
            >
                <div class="pl-1">
                    <strong>Mash Potatoes</strong><br />12:30 - 3:30p
                </div>
            </div>
        </div>
    </div> -->
</template>

<script lang="ts">
import {Vue, Prop, Component, Emit} from "vue-property-decorator";

@Component({
    name: "List"
})
export default class List extends Vue {
    @Prop(Number) numCols: number | undefined;
    @Prop(Array) items: Array<any> | undefined;
    @Prop(Number) listId: number | undefined;

    top: string = "250px";
    myClass: string = "";
    mouseDownOn: string = "";
    id: string = "";
    isDragging: boolean = false;

    created() {
        let id = Math.random().toString();
        this.id = id;
    }

    ensureMouseEvent(event: MouseEvent) {
        if (!event) {
            event = window.event as MouseEvent;
        }
    }

    mouseDown(event: MouseEvent): any {
        this.ensureMouseEvent(event);
        this.isDragging = !this.isDragging;

        let target = event.target as HTMLElement;
        let parent = target.parentElement as HTMLElement;
        this.mouseDownOn = target.id;

        if (this.isDragging) {
            parent.addEventListener("mousemove", this.mouseMove);
        } else {
            parent.removeEventListener("mousemove", this.mouseMove);
        }
    }

    mouseMove(event: MouseEvent) {
        this.ensureMouseEvent(event);

        let target = event.target as HTMLElement;

        let parentRect = (target.parentElement as HTMLElement).getBoundingClientRect() as DOMRect;

        let clientY = event.clientY - parentRect.y - 10;
        // this.top = clientY.toString() + "px";

        this.$emit('update-time', clientY.toString() + "px", this.mouseDownOn, this.listId);
    }

    mouseUp(event: MouseEvent) {
        this.ensureMouseEvent(event);
        let target = event.target as HTMLElement;
        this.mouseDownOn = target.id;
    }
}
</script>

<style lang="scss" scoped>


.wrapper {
    position: relative;
    height: 600px;
    width: 100%;
    // background-color: aliceblue;

    .time-box {
        height: 60px;
        border-bottom: solid gray 1px;
        border-left: solid gray 1px;
    }

    .event-wrapper {
        position: relative;
    }

    .box {
        background-color: rgb(154, 208, 255);
        position: absolute;
        width: calc(100% - 10px);
        border-radius: 5px;
        min-height: 30px;
    }
}
</style>
