# plant

A website app to manage backyard orchards and anything else you can grow
in your yard.

* [Project Objectives](#objectives)
  * [Versions](#versions)
  * [Questions](#questions)
* [For Developers](#for-developers)
  * [Architecture Notes](#architecture)
  * [Developer Setup](#developer-setup)

# Objectives

* Allow users to track the plants that they're growing.
  * Provide stats on growth rates.
  * Pull in weather information.
  * Compare against other growers.
* Allow users to research plants to grow.
  * Users can search within a radius of their location for plants others are
  growing.
  * Users can determine likelihood of success.
* Assist users in management of their plants.
  * Send alerts to users when action needs to be taken based on time-of-year
  or on weather. For example, should prune/fertilize on X Date, or "there's
  a freeze warning, you need to protect your avocado tree."
* Usability
  * Users should be able to post entries about a tree from their yard on a smart
  phone.
  * Users should be able to take photos and add them to a plant entry from
  their smart phone while making a post.
  * Users should be able to operate the app while disconnected with syncing
  done later.

## Versions

## 0.0.1 MVP

* User can create an account using OAuth from their Google account.
* User can add/delete/update each plant in their yard.
* User can add entries to each plant. Each entry will have a date and
details.

## 0.0.2 and beyond

* Add features/fields to user's account.
  * Add Facebook as OAuth option.
  * Allow user to add their GPS location to their account.
* Add features to a plant post.
  * Allow photos to be added.
  * Add markdown for details to allow for formatting.
* Add structured fields for each plant.
  * Dates for planting, germination.
  * Multi-bud - treat each scion as its own tree but group on this.
  * Perennial/annual (other?)
* Add structured fields for data entry posts.
  * E.g. height, width etc. to calculate growth rates.
  * Applications of fertilizer, mulch etc for reporting on growth effectiveness.
  * Start and end dates for harvest. (Allow for reporting on year round
    production and prediction.)
  * Volume harvested.
* Perform calculations on entries to show changes. e.g. growth in gallons per
week.
* Use user's GPS location to pull in weather data from date of first plant
entry to current date.
* Keep user's weather data up-to-date.
* Use user's GPS location to allow them to compare their plants to the same
plants in nearby locations.
* Allow users to add parentage/genealogy to their plants.
  * i.e. if another user gave them a plant or they planted another plant from
  one that they're already documenting on the system then they can link a parent
  plant.
* Support multi-bud trees.
  * Allow for structured data entry for root stock(s) and multiple scions.
  * Allow dates for adding scions to trees.
* Allow for termination date of plants.
  * Distinguish between perennial and annuals. i.e. plants that are designed
  to die annually and those that aren't. Helps in reporting life and reason
  for death or disposal of perennial.
* Search
  * User can find a male pollinator for their female plant within a certain
  radius of their location.

## Questions

If you have questions or want to communicate with the maintainers of the
project then please [create an issue](https://github.com/guyellis/plant/issues).

# For Developers

## Architecture

### Components

#### plant

Components in the `/app/components/plant` folder.

Component naming uses CRUD (Create, Read, Update, Delete) names to identify what the component does.

* Plant
  * Container for showing and managing a single plant
  * All other components in this section are used by the Plant component directly or indirectly. i.e. Plant is the top parent
* PlantRead
  * Shows the details of the Plant
  * PlantCreateUpdate hidden
* PlantCreateUpdate
  * Create or Update a Plant.
  * PlantRead hidden
* Notes
  * Manages the Hide/Show "add note" functionality
  * Container to show a list of Notes
* NoteCreateUpdate
  * Create or Update a Note.
* NoteRead
  * Shows the details of a Note

#### plants

Components in the `/app/components/plants` folder.

Components for managing a collection and the listing of plants.

## Developer Setup

Copy the [secrets-example.js](lib/config/secrets-example.js) file to `secrets.js` in the same directory.

Edit the `secrets.js` file and fill in the missing data. You will need to setup an application with Facebook and an account with IBM's Cloudant. At the time of writing this both were free and IBM allowed up to $50/month of Cloudant usage without charge.

### Facebook

(As with any site, the layout and options change over time so these instructions are an approximation.)

* Go to [developers.facebook.com](https://developers.facebook.com/) and on the menus click on `My Apps` and then select `Add a New App`.
* Select a WWW Website.
* Add a name (Plant is good) and click `Create New Facebook App ID`.
* There's a button to the top right to `Skip Quickstart` - hit that.
* You should end up on the Dashboard. From here you want the `App ID` and `App Secret`. Fill those in the `secrets.js` file under `clientID` and `clientSecret`.

### Cloudant

* Setup an account at [Cloudant](https://cloudant.com/)
* In the `secrets.js` file use the same `account` and `password` that you used to register on the Cloudant site.
* For dbName enter anything you want: `plant-dev` is a good choice.
* You don't need to create the DB in the Cloudant dashboard. When the app tries to access your Cloudant account it will create the DB if it can't find it.

### Running the site

* Clone the repo locally.
* As you'd expect: `npm install`
* `npm install -g nodemon`
* Terminal Window #1: `DEBUG=plant:* nodemon index.js`
  * Starts the server on port 3000
* Terminal Window #2: `npm start`
  * Starts the Webpack Dev Server on port 8080
* Navigate: [http://localhost:8080](http://localhost:8080)
