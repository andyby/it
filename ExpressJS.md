# ExpressJS notes

## send single static file
   app.get('/', (req, res) => {
   
        res.sendFile(path.join(__dirname, 'index.html'))
        
   })
   
## serve static folder
   app.use(express.static(path.join(__dirname, 'public')))
