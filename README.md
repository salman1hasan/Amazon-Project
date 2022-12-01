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

16.Add footer and add ALL RIGHTS RESERVED to the footer.  
 
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
 
 
 
1.Import NextLink from nextjs(Ignore this though because wrapping it around Link for some reason causes an error and I don’t know why hes wrapping nextlink and link, as this is causing a hydration error. (This might become an issue later but at the moment it isn’t) 
 
2.if you add it then it will be converted as href 
 
3.Go to classname and add brand and then from there add brand styling  
<Typography className={classes.brand}>amazona</Typography> 
 
4.Go to classname and add brand and then from there add brand styling  
navbar: { 
backgroundColor: '#203040', 
'& a': { 
color: '#ffffff', 
marginLeft: 10, 
}, 
}, 
brand: { 
fontweight: 'bold', 
fontSize: '1.5rem', 
}, 
 
5.Add a flexgrow to 1 and then add link href of cart and login, again the issue is nextlink and wrapping link maybe its my server or something. 

Route Product Page
Route Product Page 
 
1.Nextlink and wrap the card action area 

2.set href to product slug and pass href <NextLink href={`/product/${product.slug}`} passHref> 

3.Nextlink and wrap the card action area 

4. Go to data.js in the utils folder and for each product set the slug 

5. Free-shirt 

6. Create a product folder and then from there create [slug] for dynamic routing 

7.Import React and import router and change slug to product screen 

8. Const router = useRouter(); 

9. Const {slug}= data.products.find(a=> a.slug===slug); 

10.If(!product){ 
return <div>Product Not Found</div> 

11. Return <div> <h1>{product.name}</h1></div> 

 
Build Product Page 
1.Open slug in product folder and add <Layout> form components folder 
 
2. Import Layout from components 
 
3.<Layout title={product.name}> 
 
4. <Layout title={product.name}> 
 
5.NextLink from ‘next/link’ 
 
6. Head and use it in the title section of <Head><title>Next Amazona</title> 
 
7. Create curly brackets {title ? `${title}-Next Amazona` : ‘Next Amazona’} title 
 
8. Add href = passhref=”” 
 
9.Div className={classes.section}> 
 
10. Const classes = useStyles from utils.styles 
 
11.Go to styles.js and go to section and for section for marginTop:10px, marginBottom:10px 
 
12. Grid container spacing={1}> and import grid 
 
13. Inside the grid define another grid and grid item md=6 
 
14. Add Image src={product. Image} set alternative text set with to width={64} 
 
15. Set layout to responsive  
 
16. Import Image from ‘next/image’ 
 
17.Import grid item md={3} xs={12}> <List></List></Grid>  
<ListItem>  
 
18. Set Category={product. Category} and add Category brand and Category Rating 
 
19.<ListItem>Description: </ListItem> 
 
20.Import typography from material ui<Grid> 
 
21.Wrap all items in typography 
 
22.Add a grid item={md} xs={12} and add <Card></Card> 
 
23.And we’re going to create a border around it 
 
24.Import card and then import <List> and a <ListItem></Listitem> and add <Grid container> and add <Grid item> and add price product.price 
 
25.Set item xs={6} and then create another one grid item xs={6} 
 
26.Add countinstock>0 available and unavailable 
 
27.Add a button and then add another button 
 
28.Add styling fullwidth variant color to add to cart 
 
29.Go to footer and add margintop:10 
 
30.Add description and meta tag to title and add a h1 tag 

Add Material Ui to our project

1.Add const theme = createMuiTheme

2.Add createMuiTheme into material-ui/core

3.Typography:{
h1:{
	fontSize:'1.6rem',
	fontWeight:400,
	margin: '1rem 0'
}
h2:{
	fontSize:'1.4rem',
	fontWeight:400,
	margin: '1rem 0'
},
}

4. Add ThemeProvider theme={theme}

5.<CssBaseline/>

6.Add a slug and add a variant 

7. Add Head and add Head  <link
            rel="stylesheet"
            href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap"
          />

8.palette: {
      type: 'light',
      primary: {
        main: '#f0c000',
      },
      secondary: {
        main: '#208080',
      },
    },

Import switch design
1.Import { createContext,useReducer} from "react"

2.export const store =  {createContext}

3.const InitialState ={
darkMode: false
}

4.Export function StoreProvider(props){
const[state,dispatch] = useReducer(reducer,initialstate)

5.Add eslint reccomended

6.  const [state, dispatch] = useReducer(reducer, initialState);

7.function reducer(state, action) { 
  switch (action.type) {
    case 'DARK_MODE_ON':
      return { ...state, darkMode: true };
    case 'DARK_MODE_OFF':
      return { ...state, darkMode: false };
    default:
      return state;
  }
}

8.Layout const {state,dispatch} = useContext()

9.Import {store} from '../utils/store'

10. type: darkMode ? 'dark' : 'light',

11.Set the darkmode to true.

12. Add a Layoutjs Switch checked={darkmode} onChange={darkmodechallenger}

13.Const darkmodechangehandler dispatch type darkmode  dispatch({ type: darkMode ? 'DARK_MODE_OFF' : 'DARK_MODE_ON' });

14.Install NPM install cookie

15. Const newDarkMode= !darkmode

16.Cookies.set('darkMode', newDarkMode ? 'ON' : 'OFF');

17.darkMode: Cookies.get('darkMode') === 'ON' ? true : false,

Connect Mongodb
1.NPM install mongoose

2.Import const connection={}

3.Add async function() {
if(connection.isConnected){
console.log('already connected')
return;
}

4.Env, browser = true, node=true

5.if(connection.isConnected){
console.log('already connected')
return;
}

6.if(mongoose.connections.length>0){
connection.isConnected= mongoose.connections[0].readyState
if(connected.isConnected===1){
console.log(use previous connection)
return 
}

7. Await mongoose.disconnect

8.const db = await mongoose.connect(process.env.MONGODB_URI); //this sets the connection
  console.log('new connection');
  connection.isConnected = db.connections[0].readyState;
}

9.async function disconnect() {
  if (connection.isConnected) {
    if (process.env.NODE_ENV === 'production') {
      await mongoose.disconnect();
      connection.isConnected = false;
    } else {
      console.log('not disconnected');
    }
  }
}


10. Add env file and connect it to mongodb

11.Check the env file with the hello


 Building out Product API

1.Product.js has a mongoose and adds mongoose then from there we add all the categories that are necessary

import mongoose from 'mongoose';

const productSchema = new mongoose.Schema(
  {
    name: { type: String, required: true },
    slug: { type: String, required: true, unique: true },
    category: { type: String, required: true },
    image: { type: String, required: true },
    price: { type: Number, required: true },
    brand: { type: String, required: true },
    rating: { type: Number, required: true, default: 0 },
    numReviews: { type: Number, required: true, default: 0 },
    countInStock: { type: Number, required: true, default: 0 },
    description: { type: String, required: true },
  },
  {
    timestamps: true,
  }
);

2.
const Product =
  mongoose.models.Product || mongoose.model('Product', productSchema);
export default Product;

3.Creates a new sentence letter and from there you can add mongoose.models.product or the mongoose.model

4.Download next-connect

5.Create a handler =nc(), while importing db from '../utils/db'

6 Import import nc from 'next-connect';
import Product from '../../../models/Product';
import db from '../../../utils/db';

const handler = nc();

handler.get(async (req, res) => {
  await db.connect();  
  const products = await Product.find({});
  await db.disconnect();
  res.send(products);
});

export default handler;

//this is used to connect the database

7.Copy the whole index.js and import it to the seed part

8. When I get to the seed from there make changes to the seed

9.import nc from 'next-connect';
import Product from '../../models/Product';
import db from '../../utils/db';
import data from '../../utils/data';

const handler = nc();

handler.get(async (req, res) => {
  await db.connect();
  await Product.deleteMany();
  await Product.insertMany(data.products);
  await db.disconnect();
  res.send({ message: 'seeded successfully' });
});

export default handler;

10.Big thing is to make sure the mongodb database is succesfully connected and readandwrite is used in your username. Other than that self explanatory section as we're using nextjs syntax to connect a database
