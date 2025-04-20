<script>
import "../app.css";
import AnimatedRectangles from "./AnimatedRectangles.svelte";
</script>

<main class="flex flex-col flex-1 p-4">
    <AnimatedRectangles rectSize={60} baseColor={[255, 99, 132]} />
    <section
        id="introPage"
        class="grid grid-cols-1 lg:grid-cols-2 gap-10 py-8 sm:py-14"
    >   
        <div class="flex flex-col lg:justify-center text-center lg:text-left gap-6 md:gap-2 lg:gap-4">
            <h2 class="font-semibold text-5xl sm:text-5xl md:text-5xl">
                <br /> <span class="poppins text-primary">Hello world!</span>
            </h2>
            <h2 class="font-semibold text-5xl sm:text-5xl md:text-5xl">
                My name is <span class="poppins text-primary">Piotr Kosowicz</span>,
                <br /> I am an:
            </h2>   
            <div
                class="flex flex-col lg:justify-center text-center lg:text-left gap-6 md:gap-2 lg:gap-10"
            >  
                <h2 class="font-semibold text-5xl sm:text-5xl md:text-5xl">
                    - <span class="poppins text-primary">IT Student</span>
                    <br />- <span class="poppins text-primary">Custom set designer</span>
                    <br />- <span class="poppins text-primary">Life-long learner</span>
                </h2>
                <p class="text-base sm:text-lg md:text-xl">
                    I constantly look for <span class="poppins text-primary">new challanges</span>, <span class="poppins text-primary">interesting projects</span> and <span class="poppins text-primary">opportunities to expad my knowledge</span>.
                    What brings me the most joy, is <u>elevating things from good enough, to <span class="poppins text-primary">as good as possible</span></u>.
                </p>
            </div>
        </div>
        <div class="relative shadow-2xl grid place-items-center">
            <img
                src={"favicon.png"}
                alt="-"
                class="object-cover z-[2] max-h-[70vh]"
            />
        </div>
    </section>
</main>