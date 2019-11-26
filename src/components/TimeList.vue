<template>
    <div class="time-list">
        <div class="times">
            <div v-for="time in times" :key="times.indexOf(time)" class="time">
                <span>
                    {{ twelveHour(time) }}
                </span>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import {Component, Prop, Vue} from "vue-property-decorator";

@Component({
    name: "TimeList"
})
export default class TimeList extends Vue {
    times: Array<String> = [];

    created(): any {
        for (let i = 0; i < 24; i++) {
            let time = i.toString();
            this.times.push(time);
        }
    }

    twelveHour(time: string): string {
        let newTime = parseInt(time);
        return ((newTime % 12) + 1).toString() + ((newTime > 10 && newTime != 23) ? "pm" : "am");
    }
}
</script>

<style lang="scss" scoped>
.time-list {
    position: relative;

    .times {
        // display: flex;
        // align-content: center;
        // justify-content: center;
        // flex-direction: column;

        .time {
            background-color: aliceblue;
            height: 60px;
            border-bottom: gray 1px solid;
            display: flex;
            align-items: flex-end;
            padding-left: 5px;

            &:last-child {
                border: none;
            }
        }
    }

    .box {
        background-color: aliceblue;
        position: absolute;
    }
}
</style>
