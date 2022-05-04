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
                percent: (person.salary / sum) * 100,
                share: (person.salary / sum) * monthly,
            });
        }
        people = [...update];
        console.log(people);
    };

    let add = () => {
        people = [...people, { name: "", salary: "" }];
    };

    const format = (val) => {
        return (
            typeof val === "number" && (Math.round(val * 100) / 100).toFixed(2)
        );
    };
</script>

<main>
    <div class="container">
        <div class="columns is-centered">
            <div class="column is-three-quarters-tablet">
                <div class="card">
                    <div class="card-content">
                        <div class="content">
                            <p class="title is-1 has-text-black">fair share</p>
                            <table class="table mx-auto">
                                <thead>
                                    <tr>
                                        <th>Name</th>
                                        <th>Salary</th>
                                        <th
                                            ><abbr title="% of Total Income"
                                                >%TI</abbr
                                            ></th
                                        >
                                        <th
                                            ><abbr title="Share of Monthly Bill"
                                                >SMB</abbr
                                            ></th
                                        >
                                    </tr>
                                </thead>
                                <tbody>
                                    {#each people as item, index}
                                        <tr>
                                            <th>
                                                <input
                                                    class="input"
                                                    bind:value={item.name}
                                                    type="text"
                                                    placeholder="Name..."
                                                />
                                            </th>
                                            <td>
                                                <input
                                                    class="input"
                                                    bind:value={item.salary}
                                                    type="number"
                                                    placeholder="Salary..."
                                                />
                                            </td>
                                            <td>
                                                {format(item.percent) || "---"}%
                                            </td>
                                            <td>
                                                ${format(item.share) || "---"}
                                            </td>
                                        </tr>
                                    {/each}
                                </tbody>
                            </table>
                            <div
                                class="columns is-mobile is-centered is-multiline is-vcentered"
                            >
                                <div class="column is-narrow">
                                    <strong> Monthly Bills:</strong>
                                </div>
                                <div class="column is-one-third">
                                    <input
                                        name="bills"
                                        class="input"
                                        bind:value={monthly}
                                        type="number"
                                        placeholder="Monthly Bills"
                                    />
                                </div>
                            </div>
                            <button class="button is-info" on:click={add}
                                >Add Person</button
                            >
                            <button
                                class="button is-success"
                                on:click={calculate}>Calculate</button
                            >
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</main>

<style>
    .title {
        font-family: "Bebas Neue", cursive;
    }
</style>
