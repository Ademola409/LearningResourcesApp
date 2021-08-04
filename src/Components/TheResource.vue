<template>
    <base-card>
        <base-button :mode='storedResButtonMode' @click='setSelectedComponent("stored-resources")'>Stored Resources</base-button>
        <base-button :mode='addResButtonMode' @click='setSelectedComponent("add-resource")'>Add Resources</base-button>
        <keep-alive>
            <component :is="selectedTab"></component>
        </keep-alive>
    </base-card>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
export default {
    components:{
       'stored-resources':StoredResources, 
       'add-resource':AddResource,
    },

    data(){
        return {
            selectedTab:'stored-resources',
            storedResources:[
                {
                    id:'official-guide',
                    title:'Official guide',
                    description: 'The official vue.js documentation',
                    link:'https://vuejs.org'
                },

                {
                    id:'google',
                    title:'Google',
                    description: 'Learn to google...',
                    link:'https://google.org'
                },
            ]
        }
    },
        
    computed:{
        storedResButtonMode(){
            return this.selectedTab==="stored-resources" ? null:"flat"
        },

        addResButtonMode(){
            return this.selectedTab==="add-resource" ? null: "flat" 
        }
    },

    provide(){
        return {
            resources:this.storedResources,
            addResource:this.addResource,
            deleteResource:this.deleteResource
        }
    },
    methods:{
        setSelectedComponent(tab){
            this.selectedTab=tab
        },

        addResource(title, description, link){
            const newResource={
                id: new Date().toISOString(),
                title: title,
                description:description,
                link:link,
            };
            this.storedResources.unshift(newResource);
            this.selectedTab='stored-resources'
        },

        deleteResource(resId){
            const resIdx=this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIdx,1);
        }
    },


}
</script>