Hello! My name is Jakub Holý and I am a full-stack Clojure(Script) developer by day and a pair-programming partner and teacher for hire by night via [my company Holy Dev](holy-dev.html).

I like to learn and think and I share a lot of that at [my blog, Holy on Dev](https://blog.jakubholy.net/), which is my primary presence on the internets and where you can also [learn more about me](https://blog.jakubholy.net/me/), should you be so inclined.

You are welcome to [contact me](contact.html).

## Latest blog posts

<section id="blogposts">
    <template id="blogpost">
    <article class="blogpost-item">
        <h3></h3>
        <time></time>
        <p class="description"></p>
    </article>
    </template>
</section>

<script>
    async function renderLatestPosts() {
        if (typeof window.DOMParser != "undefined") {
            const xmlStr = await fetch('https://blog.jakubholy.net/feed.xml').then(r => r.text())
            const xml = (new window.DOMParser()).parseFromString(xmlStr, "text/xml");    
            const items = xml.getElementsByTagName('item');
            for (let i = 0;i < Math.min(3,items.length); i++) {
                // Get content
                const item = items.item(i);
                const description = item.querySelector('description').textContent;
                const link = item.querySelector('link').textContent;
                const pubDate = item.querySelector('pubDate').textContent.substr(0,16); // w/o time
                const title = item.querySelector('title').textContent;
                // Display
                const tpl = document.querySelector('#blogpost');
                tpl.content.querySelector('h3').textContent = title;
                const elmDescr = tpl.content.querySelector('.description');
                elmDescr.textContent = description + ' ';
                const elmLink = document.createElement('a');
                elmLink.href = link; elmLink.textContent = 'Continue reading...'
                elmDescr.appendChild(elmLink);
                tpl.content.querySelector('time').textContent = pubDate;
                const clone = document.importNode(tpl.content, true);
                document.querySelector('#blogposts').appendChild(clone);
            }

            const elmLink = document.createElement('a');
            elmLink.href = 'https://blog.jakubholy.net/'; 
            elmLink.textContent = `See all ${items.length} posts`
            document.querySelector('#blogposts').appendChild(elmLink);
        };
    }
    renderLatestPosts(); 
</script>