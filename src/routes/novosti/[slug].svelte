<script context="module">
    export async function preload({params}) {
        const res = await this.fetch(`novosti/${params.slug}.json`);
        const data = await res.json();
        if (res.status === 200) {
            return { item: data };
        } else {
            this.error(res.status, data.message);
        }
    }
</script>

<svelte:head>
    <title>CZA Osijek | {item.title}</title>
</svelte:head>

<script>
    import BlogArticle from "../../shared/components/BlogArticle.svelte";
    import Title from "../../shared/components/Title.svelte";
    import Content from "../../shared/components/Content.svelte";

    export let item;
</script>

<section class="grid generic-section">
    <div class="col-6 col-m-8 col-s-10 col-xs-12">
        <BlogArticle>
            <time>{item.date}</time>
            <Title>{item.title}</Title>
            <Content>
                {@html item.content}
                <p>Slike možete pogledati u našoj <a href="/galerija/{item.gallery}">galeriji</a>.</p>
            </Content>
        </BlogArticle>
    </div>
</section>
