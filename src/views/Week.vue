<template>
    <div class="week">
        <time-list />
        <list :items="testList[0]" :listId="0" @update-time="udpateTime" />
        <list :items="testList[1]" :listId="1" @update-time="udpateTime"/>
        <list :listId="0" @updateTime="udpateTime"/>
        <list :listId="0" @updateTime="udpateTime"/>
        <list :listId="0" @updateTime="udpateTime"/>
        <list :listId="0" @updateTime="udpateTime"/>
        <list :listId="0" @updateTime="udpateTime"/>
    </div>
</template>

<script lang="ts">
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import List from "@/components/List.vue";
import TimeList from "@/components/TimeList.vue";
import {Component, Prop, Vue} from "vue-property-decorator";

@Component({
    name: "Week",
    components: {
        List,
        TimeList
    }
})
export default class Week extends Vue {
    testList = [
        [
            {
                name: "day one",
                id: "test-one",
                time: "230px"
            }
        ],
        [
            {
                name: "day two",
                id: "test-two",
                time: "230px"
            }
        ]
    ];

    public test(param: any): any {
        return "this is a string";
    }

    udpateTime(time: string, itemId: string, listId: number): void {
        let events = this.testList[listId];

        for (let i = 0; i < events.length; i++) {
            let event = events[i];

            if (event.id === itemId) {
                event.time = time;
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.week {
    overflow: auto;
    height: 500px;
    background-color: aquamarine;
    display: flex;
    // padding: 200px;
}
</style>
