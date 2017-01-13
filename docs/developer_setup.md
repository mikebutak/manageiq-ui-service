# Developer Setup

Logging in to the SUI requires a running instance of ManageIQ. Instructions on how to install ManageIQ can be found
[here](https://github.com/ManageIQ/guides/blob/master/developer_setup.md).

### Install Repository and Prerequisites

- Have the [ManageIQ](http://github.com/ManageIQ/manageiq) repo cloned into a
  directory named `manageiq`, and ready to be started. See [here](https://github.com/ManageIQ/guides/blob/master/developer_setup.md)
  for the steps required to setup ManageIQ.
- Have the SUI repo at the same level as `manageiq/`, this ensures the SUI builds, `yarn run build`, into the correct manageiq folder.
  - `git clone git@github.com:ManageIQ/manageiq-ui-service.git`.
- Have nodejs **v6.x** and npm **3.x.x** installed (npm should be installed with NodeJS)
- If using [nvm](https://github.com/creationix/nvm) you can ensure you are using the correct node version with `nvm use`
- Have yarn (^v0.16.1) and gulp globally installed.
  - `npm install -g yarn gulp`
  - Be sure to periodically update with `yarn self-update`

### Install Dependencies

- `cd manageiq-ui-service`
- `yarn install`

### Setup

- From the `manageiq-ui-service` directory, build the production version of
  the SUI. This task  will compile the assets and drop them into the `manageiq/public/ui/service` directory.
  - `yarn run build`
- If you already have `manageiq` core running on port `:3000` you can verify that the build worked correctly by visiting:
	-  [http://localhost:3000/ui/service/login](http://localhost:3000/ui/service/)


### Development

- From the `manageiq` directory, start the ManageIQ application to initiate the server listening on
http://localhost:3000 order and serve up the REST API.
  Either one of the following commands can be used.
  - `bin/rails s`
  - `MIQ_SPARTAN=minimal rake evm:start` (websockets may not work correctly)

- From the `manageiq-ui-service` directory, start the development version of
  the service UI, which will initiate the UI listening on _http://localhost:3001_, and talking to the REST API at
  _http://[::1]:3000_.  This command will also open a browser page to  _http://localhost:3001/login_.
  - `yarn start`
- If you have a local copy of Manage IQ Server installed and would like to start it up at the same time you bring up the service ui web server, run
	- ``` gulp start-manageiq-server ```

If you would like to override the default port (3000) that ManageIQ runs on you can set an environmental variable ``` export MANAGEIQPORT=4000```.
If you are running manageiq in a folder other than _../manageiq/_ then you can override this path set in _gulp/config.js_ and update the _manageiqDir_ variable path.