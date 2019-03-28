### OpenY PEF GXP Sync

Synchronizes Groupex schedules to PEF.

### Quick start

#### Configure OpenY GXP module

Go to `/admin/openy/integrations/groupex-pro/gxp`.

1. Set up your GroupExPro client id.
2. Provide parent activity ID. Should be Group Exercises under Fitness.

#### Setup production mode

By default the module operates in demo mode.
While synchronisation in demo mode syncer proceeds the only first 5 class items for each found location.

In order to switch production mode on set the next config:

    \Drupal::configFactory()->getEditable('openy_pef_gxp_sync.settings')->set('is_production', TRUE)->save(TRUE);

### How the syncer works

The syncer consists of the next steps:

  1. Fetcher - fetches data from GroupEx API.
  2. Wrapper - prepares data for saving (maps location ids, fixes title encoding problems, etc).
  3. Wrapper - groups all items by Class ID and Location ID, calculates hash for all classes with the same ID and location.
  4. Saver   - saves sessions and mapping entities.
  5. Saver   - checks the hash and removes all entities for Class ID + Location. Create new ones.
