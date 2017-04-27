/**********************************************************

PUSHING AN EVENT INTO A GA GOAL USING GTM
by Robert Chan

**********************************************************/

**1) Create a trigger in GTM if the event needs to be filtered by page**

Title
Page View - Eligibility Page Results - GTM Load

Trigger type
Custom Event

Event name
gtm.load

Page Path contains
/xxxx/xxxxx

**2) Using GTM, make a datalayer push in Tags. The trigggering in that tag filters by page.**

Example:

Title
Custom - Event - Eligibility Check Result - Primary Eligibility Check (Tags)

HTML
<script>
  try {
    if({{ParseInt Eligibility}} === 1){
      dataLayer.push({
        'event': 'GAEvent',
        'eventCategory': {{Eligibility Check Result - Category Name}},
        'eventAction': 'PrimaryEligibilityCheck',
        'eventLabel': 'EligibilityStatus',
        'eventValue': {{ParseInt Eligibility}}
      });
    }
  }
  catch(e){}
</script>

Triggering
Page View - Eligibility Page Results - GTM Load

**3) Create a custom goal in GA**

Example:
Goal setup: custom
Goal description Type: Event
Goal details: Category, Action, Label, and Value match what we push in GTM