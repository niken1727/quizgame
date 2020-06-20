<template>
    <div>
        <h1 v-if="show" id="test">Hello from Home Compo.</h1>
        <h1 v-if="show">{{data}}</h1>
        <table border="1">
            <tr>
                <td>
                    Id
                </td>
                 <td>
                    Name
                </td>
            </tr>
              <tr v-for="user in users" :key="user.id">
                <td>
                    {{user.id}}
                </td>
                 <td>
                    {{user.name}}
                </td>
            </tr>
        </table>
        <input v-model="greeting"/>
        <button v-on:click="hello">Click</button>
    </div>
</template>
<script>
export default {
    name: 'Home',
    props:{
        data: String
    }, data(){
        return{
            greeting: "Hello",
            show: true,
            users :[
                {id: "1", name: "Nike"},
                {id: "2", name: "Nikee"},
                {id: "3", name: "Niken"}
            ]
        }
    }
    ,methods:{
        hello(){
            alert("hello")
        }
    }
}
</script>
<style scoped>
#test {
    color: green;
}
</style>