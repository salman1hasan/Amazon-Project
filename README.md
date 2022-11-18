Salman Hasan 
11/16/2022 
 
New Amazona Project 
Ran into some errors with the old one, so I thought I'd try to make a new one 
 
Important notes when I make the project better 
Material UI is being used for this project, in my previous project I used NextJS and SCSS which was good. I added a customized navbar with scss styles, material ui can be used with it as well. 
 
Implement custom navigation bar the way I had it and import it into the Layout file 
 
Create Next App 

Section 1-Create Next App 

1.NPX Create react app 
2.Next-Amazona 
3.Add ES.LINT 
4. Add all dependencies needed as well 
5.NPM Run dev 

6.Install NPM Material UI 
Ran into an error here but I fixed it with a fix-the-upstream-dependency 
https://stackoverflow.com/questions/64936044/fix-the-upstream-dependency-conflict-installing-npm-packages 
 

7.Delete everything from the Index.js 
<Layout> 

<h1> 
<ul> 
	<li>   </li> 
	<li>   </li> 
	<li>   </li> 
</ul> 
</h1> 
</Layout> 
 

8. Components and add a layout file  
Ran into an error with React 
https://stackoverflow.com/questions/68163385/parsing-error-cannot-find-module-next-babel 

9. RFC and create a file and import a header and import amazona 
10. <title>Next Amazona</title> 

11.App bar”Position” -Static 

12.Import App bar and tool bar 
13.Toolbar and typography 
14.Add Container and add children Container {Children} 
15.Import children  

16. Add footer and add ALL RIGHTS RESERVED to the footer.  
 
Add styles to app 
1.Add styles to our amazona project 
2.Similar to css use a style called make styles from material ui 
3.Create a utils and add styles.js 
4.Add const useStyles = makeStyles and add import {makeStyles} from “@material-ui/core” 
5.const useStyles = makeStyles({ 
	navbar:{ 
		backgroundColor: ‘#203040’ //use hashtag for color and camalcase 
		‘& a’:{ 
			color: ‘#ffffff’, 
		              marginLeft: 10, 
			   
		}, 
	}, 
}); 
6. Export default useStyle 
7.Go to layout and import useStyles from ‘../utils/styles’; 
8.Import const classes = useStyles(); 
9.Go to AppBar and set a classname = {classes.navbar} and the color changes 
10.Go to styles and add main and add minHeight’80vh’ 
11. And add className={classes.main} and adds a space 
12.Go to styles for footer and set textAlign: ‘center 
13. Go to footer and classname and set it = classes.footer 

Fixing the material UI SSR issue 
1. Go to useEffect(()=> { 
		const jssStyles = document.querySelector(‘#jss-server-site’) 
},[]); 
2. If this condition exists{ 
just remove it. 
3. useEffect(() => { 
const jssStyles = document.querySelector('#jss-server-side'); 
if (jssStyles) { 
jssStyles.parentElement.removeChild(jssStyles); 
} 
}, []); 
 
4. Make an _document.js in the pages file, this changes the way our pages render using next.js 
5. Export default class MyDocument extends Document {} 
6. Have to import document from ‘next/document’ 
7. Return ( <html> which imports to ‘next/document’ 
8. render() { 
return ( 
<Html lang="en"> 
<Head></Head> 
<body> 
<Main /> 
<NextScript /> 
</body> 
</Html> 
); 
} 
} 
9.Inside the body section going to render the main and nextscript 
10.Next step is going to be initializing get initial props 
11. MyDocument.getInitialProps = async (ctx) => { 
const sheets = new ServerStyleSheets(); 
const originalRenderPage = ctx.renderPage; 
ctx.renderPage = () => { 
return originalRenderPage({ 
enhanceApp: (App) => (props) => sheets.collect(<App {...props} />), 
}); 
}; 
const initialProps = await Document.getInitialProps(ctx); 
return { 
...initialProps, 
styles: [ 
...React.Children.toArray(initialProps.styles), 
sheets.getStyleElement(), 
], 
}; 
}; 
12.Import serverstylesshets which comes from materialui core 
13.Get originalrenderpage from ctx render.page and change render page function 
14.ctx.renderpage = call original is an object with enhanceapp accepts app as a parameter, which returns props as another function and add sheets.collect and return the app with props as a parameter 
15.Const initialProps = await document.getinitialprops(ctx) 
16.All elements need to be returned in initial props and have to add styles 
17.Add react children.toArray and add initialprops and sheets.get style element();
