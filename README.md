# Store Visit Conversions: The Ghost in the Omnichannel Machine

Google says its store visit conversions are **99%** accurate. Read that number again, because it is doing a lot of quiet work. It does not mean **99%** of the visits were caused by your ad. It does not mean **99%** of those visitors bought anything. It means that when Google's model says a person walked into a store, it is **99%** confident a person walked into a store. That is the whole claim. Everything else, you are inferring.

I have managed retail and omnichannel ad accounts long enough to watch this metric quietly reshape how budgets get set. And in 2026 Google started auto-enabling store visit conversions in accounts that never asked for them. So your reported ROAS went up, your campaigns started optimising toward something new, and most teams never noticed the floor shift under them.

This is not a post about whether store visit conversions are real. They are real, in the sense that the modeling is genuine and the methodology is sophisticated. This is a post about what the metric actually measures versus what Smart Bidding treats it as - and the gap between those two things is where your ad spend goes to die.

The short version: store visit conversions are estimated, not counted. When you let Smart Bidding optimise toward an estimate of foot traffic instead of actual revenue, you are training an algorithm on a statistical proxy that may have no relationship to sales. DataCops exists because the fix is architectural - you control what signal reaches the algorithm, and you make sure it is real revenue, not modeled ghosts.

## Quick stuff people keep asking

**How does Google measure store visit conversions from ads?** It uses anonymised, aggregated location data - GPS, Wi-Fi, and Bluetooth signals from users who have Location History on - matched against your store's mapped coordinates. Then it extrapolates from that sampled, opted-in panel to your full ad audience using statistical modeling. You are not seeing counted visits. You are seeing a model's estimate.

**Are Google Ads store visit conversions accurate?** Accurate at the thing they measure: did a device enter a mapped location. Not accurate at the thing you care about: did my ad cause that visit, and did that person spend money. Those are different questions, and the **99%** figure only answers the first one.

**Why did Google automatically enable store visit conversions in my account?** Because Google rolled out auto-enablement across eligible accounts in 2026. If your campaigns suddenly show more conversions and a healthier ROAS with no change on your end, check your conversion actions. This is the most likely cause.

**Can store visit conversions inflate my ROAS numbers?** Yes, directly. Store visits get counted as conversions, often with an assigned value. Add a modeled, estimated conversion type to your conversion column and the reported total climbs, even though your bank balance did not. Reported ROAS goes up. Actual ROAS does not move.

**What data does Google use to track if someone visited my store?** Aggregated location signals from users with Location History enabled, blended with query data, ad interaction data, and Google's maps of physical store locations. It is a panel-and-model approach, not a per-person ledger.

**How do I measure online-to-offline conversions accurately?** Honestly, you cannot get to true accuracy with modeled visit data alone. The closest thing is connecting actual point-of-sale revenue back to ad exposure - Meta's Offline Conversions API and Google's offline conversion imports both do a version of this. Revenue you can verify beats visits you can only estimate.

**Does Meta have a way to track in-store visits from ads?** Meta's Offline Conversions API connects in-store purchases - real transactions - back to ad exposure. That is a stronger signal than a visit estimate, because it is anchored to money, not to a device crossing a geofence.

**What is a good store visit conversion rate for retail advertising?** Anyone quoting you a clean benchmark is quoting you a number built on modeled data. Treat store visit rate as a directional trend, not a hard KPI. The benchmark that matters is offline revenue per ad dollar, and that you measure yourself.

## The gap: estimated visits are not measured sales

Here is the structural problem, and it is Layer 4 of how ad data goes wrong - the quality of what is being collected.

Store visit conversions are a model output. Google takes a panel of opted-in, Location-History-on users, observes their movements, and extrapolates to your whole audience. That extrapolation is a statistical proxy. It is a good one. It is still a proxy. And a proxy carries two kinds of error that the **99%** headline never mentions.

First error: visit attribution is not causal attribution. The model can tell you a device that saw your ad later entered a store. It cannot tell you the ad caused the visit. The person may have been driving past anyway. They may shop there weekly. They may have searched your brand because they were already going. Google's **99%** confidence is about detection - did the device enter the geofence - not about causation. Smart Bidding does not make that distinction. It treats the modeled visit as a conversion and bids toward it.

Second error: a visit is not a sale. Foot traffic and revenue are correlated, loosely, in a healthy retail business. They are not the same thing. Someone walks in, browses, uses the bathroom, returns an item, leaves. That is a counted store visit. It is not a dollar. When your campaign optimises for visits, it optimises for the door, not the till.

Now stack auto-enablement on top. Google switched this on in accounts that never opted in. The reported conversion count rose. Smart Bidding - tROAS and Performance Max store goals especially - does not optimise toward your intentions. It optimises toward the conversion signal in the account. Add a modeled visit signal and the algorithm starts steering spend toward whatever traffic patterns produce modeled visits. Not buyers. Visit-shaped behaviour.

Here is the moment that makes it concrete. Picture a regional retailer that let auto-enablement ride for a quarter. Performance Max with store goals turned on. The dashboard looked fantastic - conversions up **40%**, ROAS up, the weekly report a wall of green. Then someone reconciled it against point-of-sale revenue. Flat. Actual sales had not moved. The algorithm had spent three months getting very, very good at buying foot traffic near stores: people who walked in, looked, and left. It optimised perfectly toward the metric it was given. The metric just was not revenue. Garbage in is generous here - it was not garbage, it was a ghost. The algorithm chased a ghost for ninety days and the budget paid for the chase.

That is the gap. Store visit conversions look like they close the omnichannel loop. They do not. They close a modeled, estimated, visit-shaped loop, and Smart Bidding cannot tell the difference between that loop and a revenue loop.

## How this compounds into Layer 5

It does not stop at one misled campaign. The modeled visit signal feeds Google's machine learning. The model learns "this audience produces store visits" and goes hunting for more audiences that look like it. If those modeled visits were partly drive-by traffic, partly people who never bought, partly noise in the extrapolation, then the algorithm is now optimising toward noise and finding more of it. Estimated in, estimated optimised, estimated out. Every budget reallocation after that - channel splits, regional weighting, bid targets - sits on a baseline you cannot verify.

The root cause is the same one behind every version of this problem. A third-party platform is collecting and modeling a signal, mixing estimate with measurement, and you have no isolation layer between that mixed signal and your bidding decisions. You inherit Google's model as truth because you have nothing of your own to check it against.

The fix is architectural. You need a first-party layer that collects what you can actually verify - real conversions, real revenue, filtered for bots and junk before it is sent anywhere - and feeds the ad platforms that clean signal. That is what DataCops does: first-party collection on your own subdomain, [bot filtering](/fraud-traffic-validation) at ingestion, and clean conversion data relayed to Meta, Google, TikTok, and LinkedIn via CAPI. It will not give you Google's modeled store visits. It gives you the thing those visits were supposed to be a proxy for - verified revenue - so the algorithm trains on sales instead of ghosts.

## Decision guide

You just noticed your conversion count jumped with no campaign change: check your conversion actions for auto-enabled store visits before you trust this quarter's ROAS.

You run physical stores and care about foot traffic as a real goal: keep store visits as a secondary, reported metric - watch the trend, never bid primarily toward it.

You run Performance Max with store goals: separate your conversion actions so revenue and visits are not summed into one number, and set tROAS against verified revenue only.

You want offline impact measured properly: use Meta Offline Conversions API or Google offline conversion imports with real point-of-sale data - money beats modeled visits every time.

You cannot tell how much of your reported ROAS is modeled versus real: that is the signal to put a [first-party data](/first-party-consent-manager-platform) layer in place, so you have your own verified baseline to reconcile against.

You are a pure e-commerce brand with no stores: ignore store visit conversions entirely, and audit whether anything else modeled is padding your conversion column.

## You are bidding on a ghost

Here is the mistake. Teams see store visit conversions in the dashboard, watch ROAS climb, and conclude the omnichannel loop is closed and the campaigns are working. What is actually happening is the algorithm has been handed an estimate and told to treat it as a sale, and it is doing exactly that - faithfully, expensively, toward the door instead of the till.

Modeled data is not a crime. Pretending modeled data is measured data is. Google never lied to you; the **99%** accuracy claim is technically true and narrowly scoped, and the word "estimated" is right there in the documentation footnote. The mistake is yours if you let Smart Bidding optimise against a proxy you never verified.

So go pull your offline numbers. Take last quarter's reported store visit conversions, take last quarter's actual point-of-sale revenue, and put them side by side. If they do not move together, ask yourself the only question that matters: how much of your ad budget is currently chasing a ghost?

---

Research by [DataCops](https://www.joindatacops.com) — first-party tracking, consent infrastructure, fraud prevention, and server-side CAPI for Meta, Google, TikTok, and LinkedIn.
