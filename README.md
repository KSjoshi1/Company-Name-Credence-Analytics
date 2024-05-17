
# Company-Name-Credence-Analytics


server.js


const mongoose = require("mongoose");
const app = express();
const Book = require('./models/Book'); // Import the model

app.use(express.json()); //Middleware to parse JSON bodies

app.listen(3000, () => {
  console.log("Server is running on port 3000");
});

mongoose connect('mongodb://localhost:27017/bookstore', {
    userNewUrlParser: true,
    userUnifiedTopology: true,
})
.then(() => console.log('MongoDB connected'))
.catch((err => console.log(err)));


app.post('/book', async (request, response) => {
    const getBooksQuery = `
    SELECT *
    FROM book
    ORDER BY book_id;
    `;

    const bookArray = await db.all(getBooksQuery);
    response.send(bookArray);
});

app.post("/books/", async (request, response) => {
    const bookDetails = request.body;
    const {
        title,
        authorId,
        rating,
        reviewCount,
        description,
        pages,
        dateDfPublication,
        editionLanguage,
        price,
        onlineStores,
    } = bookDetails;
    const addBookQurey = `
    INSERT INTO
    book (title, author_id,rating,rating_count,review_count, description,pages,date_of_publication,edition_language,price,online_stores,)
    VALUES
    (
        '${title}',
        '${authorId},
        '${rating},
        '${ratingCount}',
        '${reviewCount}',
        '${description}',
        '${pages}',
        '${dateDfPublication}',
        '${editionLanguage}',
        '${price}',
        '${onlineStores}',
    );
    `;
    const dbResponse = await db.run(addBookQurey);
    const bookId = dbResponse.lastID;
    response.send({ bookId: bookId});
});

app.get("/books/:bookId/", async (request, response) => {
    const { bookId } = request.params;
    const getBookQuery = `
    SELECT
    *
    FROM
    book
    WHERE
    book_id = ${bookId};
    `;

    const book = await db.get(getBookQuery);
    response.send(book);
});
