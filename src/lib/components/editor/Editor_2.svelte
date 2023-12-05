<script>
    import 'grapesjs/dist/css/grapes.min.css';
    // import  "grapesjs-tailwind/dist/grapesjs-tailwind.min.js"
    // import "grapesjs-tailwind/dist/grapesjs-tailwind.min.js.map"
    import grapesjs from 'grapesjs';
    import { onMount } from 'svelte';

    let editor ;
    onMount(()=>{
        editor = grapesjs.init({
        // Indicate where to init the editor. You can also pass an HTMLElement
            container: '#gjs',
            // Get the content for the canvas directly from the element
            // As an alternative we could use: `components: '<h1>Hello World Component!</h1>'`,
            fromElement: true,
            // Size of the editor
            height: '500px',
            width: 'full',
            // Disable the storage manager for the moment
            storageManager: false,
            // Avoid any default panel
            // panels: { defaults: [] },

            blockManager: {
                    appendTo: '#blocks',appendOnClick:"#blocks",
                    blocks: [
                    {
                        id: 'section', // id is mandatory
                        label: '<b>Section</b>', // You can use HTML/SVG inside labels
                        attributes: { class:'gjs-block-section' },
                        content: `<section>
                        <h1>This is a simple title</h1>
                        <div>This is just a Lorem text: Lorem ipsum dolor sit amet</div>
                        </section>`,
                    }, {
                        id: 'text',
                        label: 'Text',
                        content: '<div data-gjs-type="text">Insert your text here</div>',
                    }, {
                        id: 'image',
                        label: 'Image',
                        // Select the component once it's dropped
                        select: true,
                        // You can pass components as a JSON instead of a simple HTML string,
                        // in this case we also use a defined component type `image`
                        content: { type: 'image' },
                        // This triggers `active` event on dropped components and the `image`
                        // reacts by opening the AssetManager
                        activate: true,
                    }
                    ]
                },
            });


            // Set the initial HTML content
      editor.setComponents("Testing Editor");
      

      // Listen for component changes
      editor.on('component:update', () => {
        let updatedHtml = editor.getHtml();
        console.log(updatedHtml)
      });
        })
</script>

<div class="min-h-screen flex flex-col items-center justify-center max-w-[2000px] w-full">
    <div id="gjs" class="w-full min-h-[80vh]">
        
    </div>
    <div id="blocks" class="bg-slate-700 w-full"></div>
</div>