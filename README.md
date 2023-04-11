# Devops


Reactjs+Docker+Jenkins+AWS Ec2:


# Docker->
Docker:
   1) Install DockerCLI in your Local system and check Docker Running Status
   2) Add Dockerfile in your project Root Directory
   3) For Docker Build : docker build . -t imageName
   4) To Run Docker : docker run <imageName>
   5) open new Terminal and run to view list of Docker image ids : docker ps
   6) To run dockerimage with Docker ID : docker exec -it DockerId
  
Sample Dockerfile:
 
![Screenshot from 2023-04-11 09-18-07](https://user-images.githubusercontent.com/89519757/231051220-33e61359-91ee-4970-b07c-c949d62c0479.png)

 # React app with Jenkins and Docker
  
 To use Travis CI just create .travis.yml :
  1) touch .travis.yml
  
  ![image](https://user-images.githubusercontent.com/89519757/231173660-8408a7fa-24d4-4df6-953f-24d6e27884b9.png)

   
 # To run Jenkins using official image from docker hub
   
   
 1) docker run --name jenkins -p 8080:8080 jenkins
 2) docker run -p 8080:8080 -v $PWD/jenkins:/var/jenkins_home jenkins
   
# To run docker registry using docker image on docker
   3) docker run -d -p 5000:5000 --restart always --name registry registry
   
   
 # To push a new image to registry
   
   4) docker pull ubuntu
   5)docker tag ubuntu localhost:5000/ubuntu
   6)docker push localhost:5000/ubuntu
# Docker compose
   1) touch Dockerfile
   ![image](https://user-images.githubusercontent.com/89519757/231203488-e37208ee-1d27-4a40-b2b9-7be06999aad3.png)
   2) touch docker-compose.yml
![image](https://user-images.githubusercontent.com/89519757/231203797-9c587897-b0f8-497c-8f46-fb89de892ef0.png)

   
 To run Docker -----> docker-compose up -d
   
 # Dockerfile.test
  
 ![image](https://user-images.githubusercontent.com/89519757/231204688-44ec4824-e2c2-4ace-b761-bf73586757e5.png)

   
 # Testing using Selenium
 
 Install Selenium 
   
   npm i selenium-webdriver chromedriver geckodriver --save
   npm i mocha --save-dev

 Create a test.js file in your Root Directory
   
 Change Package.json   "s-test": "mocha test"
 
 To Run Test  npm run s-test
 
 
 # Sample Test Unit
   
 /**
 * Dependency Modules
 */
var assert = require("assert").strict;
var webdriver = require("selenium-webdriver");
require("geckodriver");

// Application Server
const serverUri = "http://localhost:3001/#";
const appTitle = "React Selenium App";

/**
 * Config for Chrome browser
 * @type {webdriver}
 */
var browser = new webdriver.Builder()
	.usingServer()
	.withCapabilities({ browserName: "chrome" })
	.build();

/**
 * Config for Firefox browser (Comment Chrome config when you intent to test in Firefox)
 * @type {webdriver}
 */
/*
var browser = new webdriver.Builder()
	.usingServer()
	.withCapabilities({ browserName: "firefox" })
	.build();
 */

/**
 * Function to get the title and resolve it it promise.
 * @return {[type]} [description]
 */
function logTitle() {
	return new Promise((resolve, reject) => {
		browser.getTitle().then(function(title) {
			resolve(title);
		});
	});
}

/**
 * Sample test case
 * To check whether the given value is present in array.
 */
describe("Array", function() {
	describe("#indexOf()", function() {
		it("should return -1 when the value is not present", function() {
			assert.equal([1, 2, 3].indexOf(4), -1);
		});
	});
});

describe("Home Page", function() {
	/**
	 * Test case to load our application and check the title.
	 */
	it("Should load the home page and get title", function() {
		return new Promise((resolve, reject) => {
			browser
				.get(serverUri)
				.then(logTitle)
				.then(title => {
					assert.strictEqual(title, appTitle);
					resolve();
				})
				.catch(err => reject(err));
		});
	});

	/**
	 * Test case to check whether the given element is loaded.
	 */
	it("Should check whether the given element is loaded", function() {
		return new Promise((resolve, reject) => {
			browser
				.findElement({ id: "sel-button" })
				.then(elem => resolve())
				.catch(err => reject(err));
		});
	});

	/**
	 * End of test cases use.
	 * Closing the browser and exit.
	 */
	after(function() {
		// End of test use this.
		browser.quit();
	});
});
   
