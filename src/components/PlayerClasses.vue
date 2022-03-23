<template>
    <div>
        <h2><img id="spell" v-bind:src="spell">Please select a spellcasting ability:</h2>
        <select v-model="playerClass" id="ClassSelect">
            <option value="">None</option>
            <option>Charisma</option>
            <option>Intelligence</option>
            <option>Wisdom</option>
        </select>
        <table id="ClassTable">
            <tr>
                <th>Class Name</th>
                <th>Hit Dice</th>
                <th>Health at First Level</th>
                <th>Saving Throw Proficiencies</th>
                <th>Spellcasting Ability</th>
            </tr>
            <tr v-for="(c,pos) in classArr.filter((x) => x.spellcasting_ability === playerClass)" :key="pos">   
                    <td>{{c.name}}</td>
                    <td>{{c.hit_dice}}</td>
                    <td>{{c.hp_at_1st_level}}</td>
                    <td>{{c.prof_saving_throws}}</td>
                    <td>{{c.spellcasting_ability}}</td>
            </tr>
        </table>
    </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import axios, { AxiosResponse } from "axios";
import { PlayerClasses, ClassList } from "@/datatypes";
@Component
export default class ClassListComponent extends Vue{
    classArr: Array<PlayerClasses> = [];
    private playerClass?:string = "";
    private readonly spell = "https://static.thenounproject.com/png/2360162-200.png"

    mounted(): void{
        this.classFilter();
    }

    classFilter(): void {
        axios
            .request({
                method: "GET",
                url: "https://api.open5e.com/classes/",
            })
            .then((r: AxiosResponse) => r.data)
            .then((r: ClassList) => {
                this.classArr.splice(0);
                this.classArr.push(...r.results);
            });
    }
}
</script>