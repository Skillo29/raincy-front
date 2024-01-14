<script>
    let email = "";
    let selectedCity = "";
    let selectedServices = [];

    const cities = ["New York", "San Francisco", "London", "Tokyo"];
    const services = ["Web Development", "Graphic Design", "Digital Marketing", "App Development"];

const apiUrl = "https://flick-back.com/alert"
    async function createAlert() {
    const postData = {
            mail: email,
            type: selectedCity,
        };
        console.log(postData)
        try {
            const response = await fetch(apiUrl, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(postData),
            });
            console.log("response",response)
            if (!response.ok) {
                throw new Error(`HTTP error! Status: ${response.status}`);
            }

            const data = await response.json();
            console.log('Response from API:', data);
            // Do something with the response data
        } catch (error) {
            console.error('Error:', error.message);
            // Handle errors
        }
    }
</script>

<style>
    @import 'tailwindcss/base.css';
    @import 'tailwindcss/components.css';
    @import 'tailwindcss/utilities.css';

    body {
        @apply bg-gray-100 flex items-center justify-center h-screen;
    }

    .container {
        @apply bg-white p-8 shadow-md rounded-md max-w-md w-full;
    }

    .input {
        @apply w-full mb-4 p-2 border border-gray-300 rounded-md;
    }

    .button {
        @apply bg-blue-500 text-white px-4 py-2 rounded-md cursor-pointer;
    }

    .select {
        @apply w-full mb-4 p-2 border border-gray-300 rounded-md;
    }
</style>

<div class="flex gap-10 justify-center">
    <div class="container">
        <h1 class="text-2xl font-bold mb-4">Choisissez votre service</h1>
        <input type="email" bind:value={email} placeholder="Enter your email" class="input" />

        <div class="mb-4">
            <label for="city" class="text-sm">Select City:</label>
            <select bind:value={selectedCity} id="city" class="select">
                {#each cities as city (city)}
                    <option value={city}>{city}</option>
                {/each}
            </select>
        </div>

        <div class="mb-4">
            <label class="text-sm">Select Services:</label>
            {#each services as service (service)}
                <label class="block text-gray-700">
                    <input type="checkbox" bind:group={selectedServices} value={service} />
                    {service}
                </label>
            {/each}
        </div>

        <button on:click={createAlert} class="button">
            Validate
        </button>
    </div>

</div>
<div class="mt-8 p-4 bg-gray-200 text-center">
<!--    <img src="path/to/your/logo.png" alt="Company Logo" class="w-16 h-16 mx-auto mb-4" />-->
    <p class="text-gray-600 mb-2">Contact us at: <a href="test:info@example.com" class="text-blue-500">info@example.com</a></p>
    <p class="text-sm">We offer a range of services to meet your needs. Contact us for more information.</p>
</div>