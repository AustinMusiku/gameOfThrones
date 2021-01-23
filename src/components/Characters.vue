<template>
    <div class="landing">
        <input @input="searching" v-model="search" type="text" class="search-bar" placeholder="Search by name or house (E.g., Snow, Arya, Targaryaen)">
        <!--<p>inputText: {{search}}</p>
        <p>filteredCharacters: {{filteredCharacters[0]}}</p>-->
        <div v-if="filteredCharacters.length" class="deck">
            <div v-for="filteredCharacter in filteredCharacters"  :key="filteredCharacter.id" class="card">
                <div class="img">
                    <img :src="filteredCharacter.imageUrl" alt="">
                </div>
                <div class="card-text">
                    <h4 class="name">{{filteredCharacter.fullName}}</h4>
                    <p class="title">{{filteredCharacter.title}}</p>
                    <p class="house">House: {{filteredCharacter.family}}</p>
                </div>
            </div>
        </div>
        <div v-else class="deck">
            <div v-for="character in characters"  :key="character.id" class="card">
                <div class="img">
                    <img :src="character.imageUrl" alt="">
                </div>
                <div class="card-text">
                    <h4 class="name">{{character.fullName}}</h4>
                    <p class="title">{{character.title}}</p>
                    <p class="house">House: {{character.family}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Characters',
    data(){
        return{
            search: '',
            characters: [],
            filteredCharacters: [],
            firstNameFilter: [],
            lastNameFilter: [],
            houseFilter: []
        }
    },
    mounted(){
        fetch('https://thronesapi.com/api/v2/Characters')
            .then(response=> response.json())
            .then(data=>this.characters=data)
            .catch(err=>console.log(err))
    },
    methods: {
        searching(){
            window.scrollTo(0, 400);
            this.firstNameFilter=this.characters.filter(item=>{
                return item.firstName.toLowerCase().startsWith(this.search.toLowerCase());
            });
            this.lastNameFilter=this.characters.filter(item=>{
                return item.lastName.toLowerCase().startsWith(this.search.toLowerCase());
            });
            this.houseFilter=this.characters.filter(item=>{
                return item.family.toLowerCase().startsWith(this.search.toLowerCase());
            });
            let filtered=[...this.firstNameFilter, ...this.lastNameFilter, ...this.houseFilter];
            console.log(this.filteredCharacters);
            this.filteredCharacters = Array.from(new Set(filtered));
        }
    }
}
</script>

<style>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.landing{
    margin: 0 auto;
    width: 900px;    
}
.search-bar{
    margin: 3em auto 5em;
    padding: 1em;
    width: 100%;
    border: none;
    outline: none;
    background-color: #333d443a;
}
.deck{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 3em;
    width: 100%;
}
.card{
    display: flex;
    flex-direction: column;
    height: fit-content;
    box-shadow: 1px 1px 50px 10px #f1f1f1;
}
img{
    height: 250px;
    width: 100%;
}
.card-text{
    padding: 1em;
    text-align: left;
}
.name{
    margin: 0 0 .5em;
}
p{
    line-height: 1.6;
    font-size: 14px;
}

</style>