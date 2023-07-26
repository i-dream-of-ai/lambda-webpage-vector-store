# Web Content Embedding Transformer

## Description

This project is a Lambda function that scrapes URLs for links and content, transforms the content into an embedding format using OpenAI, and stores the embeddings in Pinecone Vector DB. The scraped links are stored in a MongoDB collection. The goal of this project is to allow users to easily transform their web content into embeddings that can be used with AI, such as a custom chatbot.

## Features

- **URL Scraping**: The function takes a list of URLs and scrapes those URLs for links that start with the original URL.
- **Content Scraping**: The function scrapes the webpages of the obtained links for content.
- **Content Chunking**: The scraped content is split into chunks.
- **Embedding Transformation**: The chunks are sent to OpenAI to be transformed into an embedding format.
- **Embedding Storage**: The embeddings are stored in Pinecone Vector DB with metadata for advanced searching, and referencing.
- **Link Storage**: The scraped links are stored in a MongoDB collection.

## Technologies Used

- **AWS Lambda**: A compute service that lets you run code without provisioning or managing servers.
- **MongoDB**: A source-available cross-platform document-oriented database program used to store the scraped links.
- **OpenAI**: An artificial intelligence research lab whose API is used to transform the scraped content into an embedding format.
- **Pinecone**: A vector database used to store the embeddings generated by OpenAI.
- **Puppeteer**: A Node library used to scrape the URLs for links and content.
- **Node.js**: An open-source, cross-platform, back-end JavaScript runtime environment used to write the Lambda function.
- **npm (Node Package Manager)**: The default package manager for Node.js, used to manage the project's dependencies.

## Getting Started

### Prerequisites

- AWS account with access to Lambda
- MongoDB account
- OpenAI API key
- Pinecone account
- Node.js and npm installed on your local machine

### Environment Variables

The following environment variables are required for the function to run properly:

- `MONGODB_URI`: Your MongoDB URI
- `MONGODB_DB`: Your MongoDB database name
- `PINECONE_INDEX_NAME`: Your Pinecone index name
- `PINECONE_ENVIRONMENT`: Your Pinecone environment
- `PINECONE_API_KEY`: Your Pinecone API key
- `OPENAI_API_KEY`: Your OpenAI API key
- `OPENAI_ORGANIZATION`: Your OpenAI organization

### Installation

1. Clone the repository to your local machine.
2. Navigate to the project directory.
3. Install the dependencies with `npm install`.
4. Set up your environment variables for AWS, MongoDB, OpenAI, and Pinecone.
5. Deploy the function to AWS Lambda.


## Usage

To use this function, provide a list of URLs as input. You will also need to provide a namespace which is used in the Pinecone DB to keep data separate and organized, as well as in a MongoDB namespace collection. The function will scrape the URLs for links, scrape the webpages for content, transform the content into embeddings, and store the embeddings and links.

- You MUST provide a namespace (string). This will be used for MongoDB AND for the Pinecone DB.
- You MUST provide a teamId (string). This will be used for MongoDB.
- If you DO provide an array of URLs, it will scrape those URLs for links for the queue.
- If you DONT provide an array of URLs, it will pull the namespace data from MongoDB and scrape the queue URLs for content. It will create vectors of that content, split them into chunks (1.MB max), then store the vector chunks + metadata (url and chuck) to Pinecone.

## Developer Documentation

This project includes a `Crawler` class that handles the scraping and processing of web content. The class includes the following methods:

- `handleRequest(url)`: This method handles the request to a URL and returns all the links on the page that start with the original URL.
- `handlePageCrawl(url, index, embedder)`: This method handles the crawling of a page. It scrapes the page for content, splits the content into chunks, transforms the chunks into embeddings, and stores the embeddings in Pinecone Vector DB.
- `crawlForUrls()`: This method handles the crawling of URLs. It adds all the URLs that have been crawled to a MongoDB collection.
- `startPageCrawl(index, embedder)`: This method starts the crawling of pages. It loads all the URLs that have been crawled into memory and starts crawling the pages.

The `Crawler` class uses several helper functions:

- `truncateStringByBytes(str, bytes)`: This function truncates a string to a specified number of bytes.
- `sliceIntoChunks(arr, maxSizeInBytes)`: This function slices an array into chunks of a specified maximum size in bytes.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT](https://choosealicense.com/licenses/mit/)