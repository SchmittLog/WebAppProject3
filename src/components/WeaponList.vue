<template>
    <div>
        <h2><img id="sword" v-bind:src="sword">Please select a weapon type:</h2>
        <select v-model="weaponType">
            <option>Simple Melee Weapons</option>
            <option>Simple Ranged Weapons</option>
            <option>Martial Melee Weapons</option>
            <option>Martial Ranged Weapons</option>
        </select>
        <table id="WeaponsTable">
            <tr>
                <th>Weapon Name</th>
                <th>Damage Dice</th>
                <th>Damage Type</th>
                <th>Properties</th>
                <th>Weight</th>
            </tr>
            <tr v-for="(w,pos) in wepArr.filter((x) => x.category === weaponType)" :key="pos">   
                    <td>{{w.name}}</td>
                    <td>{{w.damage_dice}}</td>
                    <td>{{w.damage_type}}</td>
                    <td>{{w.properties}}</td>
                    <td>{{w.weight}}</td>
            </tr>
        </table>
    </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";
import axios, { AxiosResponse } from "axios";
import { WeaponList, WeaponDetails } from "@/datatypes";
@Component
export default class WeaponListComponent extends Vue{
    wepArr: Array<WeaponDetails> = [];
    private weaponType?:string = "Simple Melee Weapons";
    private readonly sword = "https://icons.iconarchive.com/icons/icons8/windows-8/256/Military-Sword-icon.png"

    mounted(): void{
        this.wepFilter();
    }

    wepFilter(): void {
        axios
            .request({
                method: "GET",
                url: "https://api.open5e.com/weapons/",
            })
            .then((r: AxiosResponse) => r.data)
            .then((r: WeaponList) => {
                this.wepArr.splice(0);
                this.wepArr.push(...r.results);
            });
    }
}
</script>