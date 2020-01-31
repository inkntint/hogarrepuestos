<template>
	<app-shell>
		<q-artefactos-del-hogar></q-artefactos-del-hogar>
		<q-climatizacion></q-climatizacion>
		<q-coccion></q-coccion>
		<q-dispensadores-y-purificadores></q-dispensadores-y-purificadores>
		<q-electrodomesticos></q-electrodomesticos>
		<q-lavado-y-secado-de-ropa></q-lavado-y-secado-de-ropa>
		<q-otros></q-otros>
		<q-refrigeracion></q-refrigeracion>
	</app-shell>
</template>

<page-query>
query {
  allGeneralSiteSettings {
    edges {
      node {
        logo(width: 150, quality: 100)
        hero_img(width: 1920)
		    hero_message
        site_url
      }
    }
  }
  allProduct {
    edges {
      node {
        id
        path
        title
        category {
          title
        }
        available
        unit_price
        images(width: 48, height: 48, fit: contain, background: "white", quality: 100)
      }
    }
  }
}
</page-query>

<script>
	import QArtefactosDelHogar from "../components/QArtefactosDelHogar";
	import QClimatizacion from "../components/QClimatizacion";
	import QCoccion from "../components/QCoccion";
	import QDispensadoresYPurificadores from "../components/QDispensadoresYPurificadores";
	import QElectrodomesticos from "../components/QElectrodomesticos";
	import QLavadoYSecadoDeRopa from "../components/QLavadoYSecadoDeRopa";
	import QOtros from "../components/QOtros";
	import QRefrigeracion from "../components/QRefrigeracion";

	export default {
		name: "Home",
		data() {
			return {
				meta: {
					title:
						"Venta y talla de miles de rocas preciosas, semipreciosas y fósiles",
					description:
						"En Esmeralda3 vendemos y tallamos todo tipo de rocas preciosas y semipreciosas, con un inventario de más de 10.000 piezas entre meteoritos, raras y más"
				}
			};
		},
		metaInfo() {
			return {
				title: this.meta.title,
				htmlAttrs: {
					lang: "es-CO"
				},
				meta: [
					{
						name: "title",
						content: this.meta.title
					},
					{
						name: "description",
						content: this.meta.description
					},
					// og / facebook
					{
						property: "og:url",
						content: this.$page.allGeneralSiteSettings.edges[0].node.site_url
					},
					{
						property: "og:title",
						content: this.meta.title
					},
					{
						property: "og:description",
						content: this.meta.description
					},
					{
						property: "og:image",
						content: `${this.$page.allGeneralSiteSettings.edges[0].node.site_url}/og.jpg`
					},
					{ property: "og:type", content: "website" },
					{ property: "og:locale", content: "es_CO" },
					// twitter
					{ property: "twitter:card", content: "summary_large_image" },
					{
						property: "twitter:url",
						content: this.$page.allGeneralSiteSettings.edges[0].node.site_url
					},
					{
						property: "twitter:title",
						content: this.meta.title
					},
					{
						property: "twitter:description",
						content: this.meta.description
					},
					{
						property: "twitter:image",
						content: `${this.$page.allGeneralSiteSettings.edges[0].node.site_url}/og.jpg`
					}
				]
			};
		},
		components: {
			QArtefactosDelHogar,
			QClimatizacion,
			QCoccion,
			QDispensadoresYPurificadores,
			QElectrodomesticos,
			QLavadoYSecadoDeRopa,
			QOtros,
			QRefrigeracion
		},
		mounted() {
			this.$store.commit("addProducts", this.$page.allProduct.edges);
		}
	};
</script>
