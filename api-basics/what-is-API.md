
## **What is an API**

- "Application Interface"
- This means, when using a browser to go to a website, then we are using the "user interface"

## **Application Interface**

- Just as using a web browser to visit a website, you can get the same information "programmatically"
- This means you can basically talk to the "websites" or "web apps" (or any other applications) through;
	- "shell scripting" 
	- python
	- or any other programming language 

>***This is only possible if that particular "web app" has exposed their API, meaning, that they have exposed their Application Interface***

- API usernames and passwords? no, when using APIs you will instead use "tokens" 
	- usually you can get your token under the "Settings" of your repositories providers (like from GitHub for example)


##### Example with Kubernetes
- When talking to Kubernetes, we use `kubectl` which is a "CLI"
- CLI is a very simple utility
- But for GitHub, the API is much simpler than its CLI
##### Example with AWS
- You could just use the "AWS CLI" (*CLI way of doing it*)
- Or, you could write a python program using the `boto3` module, and use to interact with AWS (*the API way*)

### API modules
- For shell scripting (like `bash`) you have the `curl` module
- For python you have the `request` module
- Or maybe even use the dedicated "Postman" application

- When using the "languages modules", you will use the "HTTP protocol" or "grcp" protocol

- And by using those modules, you will directly talk to an application, meaning you will not need to use a web browser


## API references

- APIs are written by the developers of the application themselves
- For any API the developers will also create the documentation and references, because without references, other engineers will not understand how to make requests to the APIs

- **For example; what is the URL of the API?**
	- and in that URL, how to get some particular information that we are looking for

#### **Should the DevOps engineers write these APIs? the answer is No.**
**As DevOps engineer, you do not write the APIs, you only use the APIs (or you consume the APIs).**
