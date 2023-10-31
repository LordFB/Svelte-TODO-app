<script>
	import { slide } from 'svelte/transition';
    let todos = [{val:'Test', completed:false},{val:'Really long test to see what happens when values overflow. Like really long, maybe even spanning three or four lines we will know when this page renders...', completed:true}];
    function addToList(){
        let input = document.querySelector('#inp');
        if ( input.value.trim().length <= 0 ) return;
        todos = [{val: input.value.trim(), completed:false},...todos]
        input.value = '';
        input.focus();
    }
    function checkEnter(e){
        if ( e.keyCode === 13 ) addToList();
    }
    function remove(i){
        todos = todos.filter( (x,_i) => _i !== i);
    }
</script>

<div id="add">
<h1>TODOS</h1>
<hr/>
    <input name="value" on:keydown={checkEnter} id="inp" type="text" />
    <button class="add" on:click={addToList}>ADD</button>
    <hr/>
</div>
<div id="wrap">
    <ul id="content">
        {#each todos as todo, i}
            <div id="row" transition:slide>
                <input type="checkbox" class="check" checked="{todo.completed}" />
                <span class="todoval">{todo.val}</span>
                <button class="remove" on:click={ ()=>{ remove(i)}}>🗙</button>
            </div>
        {/each}
    </ul>
</div>

<style>
*{
    margin:0;
    padding:0;
}
button{
    appearance:none;
    padding:5px 10px;
    border:0;
    background:#FFF;
    border-radius:5px;
    cursor:pointer;
}
input[type=text]{
    padding:5px 10px;
    border:0;
    border-radius:5px;
    margin:25px 10px;
}
    #wrap{
        display:flex;
        width:400px;
        flex-direction:column;
    }
    .todoval{
        display:block;
        padding:20px 15px;
        list-style:none;
        flex-grow:1;
    }
    #row{
        display:flex;
        width:100%;
        align-items:center;
        border-bottom:1px solid #FFF;
    }
    .check{
        display:block;
        min-width:25px !important;
        height:25px;
        cursor:pointer;
    }

    .add{
        background:#b7ce77;
        color:#FFF;
        font-weight:600;
    }
    .remove{
        background:#ec6064;
        color:#FFF;
        padding:5px;
        min-width:25px;
        height:25px;
        line-height:20px;
        padding:0;
        font-weight:600;
    }
</style>