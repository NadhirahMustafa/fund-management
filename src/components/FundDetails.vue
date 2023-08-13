<template>
    <p>
        Funding details here
    </p>
    <p>
    <table>
        <thead>
            <th>Fund Name</th>
            <th>Description</th>
            <th>Investment type</th>
            <th>Performance History</th>
            <th>Current NAV</th>
        </thead>
        <tbody>
            <tr v-for="fundList in fundListing" :key="fundList.id">
                <td>
                    {{ fundList.fundName }}
                </td>
                <td>
                    {{ fundList.description }}
                </td>
                <td>
                    {{ fundList.investmentType }}
                </td>
                <td>
                    {{ fundList.performanceHistory }}
                </td>
                <td>
                    {{ fundList.currentNAV }}
                </td>
            </tr>
        </tbody>
    </table>
    </p>
</template>
  
<script>
import fundData from '../assets/fundList.json'
export default {
    name: 'FundDetails',
    data() {
        return {
            fundListing: fundData,
        };
    },
};
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>
  