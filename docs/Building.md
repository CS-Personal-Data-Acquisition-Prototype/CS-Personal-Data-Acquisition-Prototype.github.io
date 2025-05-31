# Building

## Local Testing

Our project can be run locally with live or static data.

- Needed repositories:
    - Rust-TCP
    - UI-Layer
    - client-api-lib
    - Pi_Transmit

<a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Rust-Tcp" target="_blank">Rust-TCP</a>

The TCP server is the heart of our project and should be set up first. Please follow the instructions in the README on the github repo to install and build. 

If testing with static data, move the data_acquisition.db file from the root directory to /src/ replacing any db file there. If testing with live data, skip this step.

Once installed, run `cargo run --features sql` and make sure the server is listening. 

<a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/client-api-lib" target="_blank">client-api-lib</a>

Next up the Client API Library should be installed. Simply install and build the project based on the instructions in the README, and make note of the location of the tcp-client folder. There is no need to run anything. 

<a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/UI-Layer" target="_blank">UI-Layer</a>

The UI layer is the front-end of our project that you will interact with. Please follow the instructions to install and build, taking care to make sure the path to the tcp-client folder is correct.

Once built, run `trunk serve` and follow the localhost link. You should now be able to interact with the website as described in the user guide on github.

If testing with static (historical) data, you are finished. Login with `testuser` and click "view" on session 2 to see data.

If testing with live data, create or log in with an existing user, making sure that sessions 1 and 2 are created. Then move on to the next step:

<a href="https://github.com/CS-Personal-Data-Acquisition-Prototype/Pi_Transmit" target="_blank">Pi_Transmit</a>

PI Transmit allows for live data (real or mock) transmission. Please follow the instructions on github to install and build.

After logging in and creating sessions 1 and 2, run Pi_Transmit. You should see a feed of live data in session 1.

## For any errors encountered, please see the troubleshooting steps for each repository on github. 


