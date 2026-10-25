### Tell me about yourself
- Victor Lee, Sophomore studying computer science at harvard
- Want to go into embedded systems programming or RTL design because I like understanding how things work

- Done research in time series foundation models for smart semiconductor manufacturing
- Enjoy the challenge of microcontroller programming, taught a class about microcontroller programming, among other things (CAD, PCB design, everything about fabrication)
- Interned at Silicon Labs, IoT, working on testing

### Why IBM?
- IBM being synonymous with innovation.
- Developing the first mass produced computers
- Learning about the IBM 360 in my computing hardware class, the first general purpose architecture.
- Seeing [A Boy and His Atom](https://www.youtube.com/watch?v=oSCX78-8-q0).
- Learning manual machining, and fell into the a rabbit hole learning about metrology. IBM developed the first scanning tunneling microscope used to look for surface quality.
- New AI era, with more innovation to come.

- This role has a bunch of specific things I'm interested in, like firmware development, RTL design and verification.
- Also caters towards a broad skillset like mines, including PCB design and CAD.

### Tell us about a time something you made went wrong and what you did to fix it.
- Originally thinking that forecasting would be easy, then I could make millions off the stock market or something.
- Forecasting not working.
- Debugging as narrowing down the scope of the issue. 
	- Attempting to clean data: garbage-in, garbage-out.
	- Testing the most simple example: a sine-wave with some noise.
	- Switching from a binning based tokenizer back to small codebook VQ-VAE (which, by nature of the coarse granularity of the autoencoder, is more tolerant)

### Tell us about your last group project
- Bending the definition for a group project.
- Roomate cleaning is arguably more important. Someone not carrying their weight? Living with these guys for the entire year, not like a group project where you can just put your head down and just do it for them.
- Taking a negotation class. Literally sitting from their perspective and realizing that they probably don't see it as an issue.
- Bringing it up while "being tough on the problem, not the people". Thanking after taking out the trash.
	- Don't make assumptions
	- Show appreciation

### What's your biggest weakness
- I think I'm too focused on little things. I want to "boil the ocean".
- I'm on the weaker side of AI tooling because I prefer to read datasheets, seek primary technical documentation, and approach things from first principles rather than prompting.
- Don't like abstracting away details. When doing research or personal projects, I even avoid using libraries.
- Honestly, not very good for productivity. Don't think I'd survive in a extremely fast environment like a startup.
- "Going against the current"

### Where do you see yourself in five years
- Hopefully building some cool, I want to have my own fabrication space!
- Working at the frontier of technology. Don't even know what my role will be, but there are too many interesting innovations out there like gate-all-around FET, TPUs (AI hardware), or high bandwidth memory. Optimizing hardware or firmware?

### What's your biggest strength
- Serious dedication to learning.
- Being able to pattern match while also absorbing a lot of information. Learning about caching in CS61 and then figuring out how to apply that to my ipod clone. Applying subword tokenization algorithm for LLMs for token compression in my time series model.

### Most challenging aspect of current project?
- Still trying to work on time series forecasting.
- Semiconductor manufacturing has very scarce public data. Need to figure out how to generate my own while maintaining complex multivariate relationships so it's not too simple to predict. Adding noise isn't a blanked solution.

- Figuring out my FPGA mouse. Making sure not to take on too much as once.
- Devkit is one thing, but I need to figure out how to route it and the peripherals I'll need. Package I want to use is BGA, so I'll need to move beyond 2-layer pcbs. Also weight reduction!!!

### Tell me about a time you met a tight deadline.
- Dire office hours from 9AM to 11PM for summer course, with Tuesday deadline I want to have some research to show for.
- Working literally whenever possible. Cutting nonessential things (ie. not having an LSTM comparison, using less noisy data, reducing sensor scope). I was able to deliver a tokenizer, even if not my ideal one. Refined it later, then it became the backbone of forecasting.
- Making sure I wasn't taking it out on the students.

### How you use AI.
- Mostly for research, don't feel comfortable letting the model code for me yet.
- Hand-rolling testbenches even if they let us use AI.
- Generate specific syntax examples, verify my understanding, bounce ideas around.
- When it comes to learning AI is a good TF, don't ask it for answers.

### Support your work after.
- For research, write a long document summarizing my findings.
- No one reads documents though, so draw diagrams with excalidraw.
- Work really is never finished.