<!-- svelte-ignore a11y-missing-attribute -->
<script>
    let monthly;
    let people = [
        { name: "", salary: "" },
        { name: "", salary: "" },
    ];

    let echo = () => {
        console.log(people);
    };

    let calculate = () => {
        const sum = people.reduce(
            (running, current) => running + current.salary,
            0
        );
        const update = [];
        for (const person of people) {
            update.push({
                ...person,
                percent: person.salary / sum,
                share: (person.salary / sum) * monthly,
            });
        }
        people = [...update];
        console.log(people);
    };

    let add = () => {
        people = [...people, { name: "", salary: "" }];
    };
</script>

<main>
    <p class="title is-1 has-text-black">Fair Share</p>
    <div class="container">
        {#each people as item, index}
            <div class="columns is-mobile is-centered is-multiline">
                <div class="column is-one-quarter">
                    <input
                        class="input"
                        bind:value={item.name}
                        type="text"
                        placeholder="Name..."
                    />
                </div>
                <div class="column is-one-quarter">
                    <div class="field has-addons">
                        <p class="control">
                            <a class="button is-static">$</a>
                        </p>
                        <input
                            class="input"
                            bind:value={item.salary}
                            type="number"
                            placeholder="Salary..."
                        />
                    </div>
                </div>
            </div>
        {/each}
        <div class="columns is-mobile is-centered is-multiline">
            <div class="column is-one-quarter">
                <div class="field has-addons">
                    <p class="control">
                        <a class="button is-static">$</a>
                    </p>
                    <p class="control">
                        <input
                            class="input"
                            bind:value={monthly}
                            type="number"
                            placeholder="Monthly Shared Bill"
                        />
                    </p>
                </div>
            </div>
        </div>
        <hr />
        <button class="button is-info" on:click={add}>Add Person</button>
        <button class="button is-success" on:click={calculate}>Calculate</button
        >
    </div>
</main>
