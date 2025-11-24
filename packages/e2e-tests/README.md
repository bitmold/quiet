## Running e2e tests locally

### Prerequisites

1. Follow the setup instructions in the root `README.md` to install dependencies and bootstrap the project.

2. Install Chromium:
   - Linux: `sudo apt install chromium-browser`
   - Mac: `brew install chromium`

3. Install electron-chromedriver globally:

`npm install -g electron-chromedriver@23.3.13`

4. Set Electron version:

`export ELECTRON_CUSTOM_VERSION=23.0.0`

### Building and Running Tests

1. In the `desktop` package, build the application:
   - Mac: `node --run distMac:local` # you may have to copy the binary from /Applications to the `e2e-tests/Quiet` directory
   - Linux: `node --run distUbuntu`

2. In the `e2e-tests` package:

`node --run linux:copy` # copy the binary to the `e2e-tests/Quiet` directory
`node --run test` # run all tests

To run individual tests:

`node --run test oneClient.test.ts`

### Known Issues & Tips

- For Mac: We may need to manually mount the .dmg and copy to /Applications (need to verify exact steps)
- For Linux: The `linux:copy` script handles moving the binary to `e2e-tests/Quiet/`
- Tests can be flaky - use the retry flag if needed: `node --run test oneClient.test.ts -- --retry 3`
- Set `DEBUG=backend*,quiet*` for more verbose logging
- The tests expect a clean state - you may need to clear application data between runs

## Test Suite

Current E2E test suite includes:
- oneClient.test.ts - Basic single client functionality
- userProfile.test.ts - User profile management
- multipleClients.test.ts - Multi-client interactions
- invitationLink.test.ts - Invitation link functionality
- backwardsCompatibility.test.ts - Version compatibility tests (CI only)

## Notes

Legacy tests pending migration can be found in commit fa1256e4d19fc481e316a09523746ce9359d4073:
- fileSending
- joiningUser
- lazyLoading
- newUser.returns