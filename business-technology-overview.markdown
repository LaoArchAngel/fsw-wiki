# Business sector

## Fsw.com
* Major functions:
 * Primary public facing ecommerce website
 * Lead generator for phone sales
* Vital to business
 * ~15% of yearly revenue
* User Count: 
 * ~33,600 sessions daily
     * ~24,462 unique users daily
       * Data courtesy Jamie Alberico
    * 40+ Sales staff (Internal)
* Key Technologies:
 * Fsw.com project(s)
     * Old site (Darwin)
          * ~3 years old
          * Inside of Fsw4.0 solution
     * New site (Archer)
          * Launched 10/2015
          * Independent repository
 * Winnowing Service 
     * Backend service that generates Darwin-era product listing pages
     * 4+ years old
 * Solr Search Service  
     * Backend Darwin era product search indexer
     * 3+ years old
 * Cart Consumer 
     * Backend service that integrates with fsw.com shopping cart process
     * Converts carts, updates inventory, auths cards, sends emails, and sends POs
     * 3+ years old
  * NightlyDbUpdates
     * Backend processes triggered on a schedule
     * Updates Incentives on Skus
     * Generates Solr Search synonyms
          * Used for matching search patterns
     * 5+ years old
  * FswAdmin.com Components (Internal tools with a UI)
     * Model Type Auto Complete Tool
         * Manages whether or not orders on Fsw.com will autocomplete (send POs without intervention by phone sales team) by item model type
         * 5+ years old
     * Marketing Content Manager
         * Manages header banners and advertisements on public Fsw.com
         * 1+ year old
     * SEO Manager 2
         * Tool for managing/manipulating how search engines rank and index our pages
         * Can set canonical, nofollow, and other SEO related aspects of public website
         * 2+ years old
 * Avalara (3rd party backend service)
     * Unseen 3rd party service/integration for getting tax rates by location a specific location
         * 3+ years old
 * Paymentech (3rd party backend service)
     * Backend service to validate/authorize credit cards and capture funds
     * Checks newly added customer credit cards for validity
     * 5+++ years old

## Phone Sales
* Major functions:
 * Convert leads
 * Maintain industry contacts
 * Follow up on Unverified Orders from fsw.com
* Vital to business
 * ~26.7% of yearly revenue
* User Count: 30
* Key Technologies:
 * FswAdmin.com Components (Internal tools with a UI)
     * Frogger
         * Order creation and editing tool
         * Generate and send quotes
         * 4+ years old
     * Odie
         * Order fulfillment tool
         * Track item/order status
         * Make Cancellations/Returns/Concessions on items and orders
         * 5+ years old
   * Async Queue Consumer
     * Backend service that integrates with Frogger and Odie
     * Updates inventory, auths cards, sends emails, and sends POs
     * 2+ years old
   * Site Search Windows Service
     * Backend search indexing service that powers:
         * Admin header search
         * Frogger product search
     * 5+ years old
 * SalesForce Windows Service
     * Backend service that provides real-time SalesForce data sync
     * 5+ years old
 * Bat Console
     * Backend service that runs every two minutes to perform SalesForce data sync in batches
     * 1 year old
 * SalesForce.com CRM (3rd party UI – Limited customization for Fsw)
     * SalesForce UI for managing contacts
     * Leads/Contacts/Accounts/Projects can all be managed in this UI
 * Avalara (3rd party backend service)
     * Unseen 3rd party service/integration for getting tax rates by location a specific location
     * 3+ years old
 * Paymentech (3rd party backend service)
     * Backend service to validate/authorize credit cards and capture funds
     * Checks newly added customer credit cards for validity
     * 5+++ years old

## National Accounts
* Major functions:
  * Maintain relationships with larger account customers
  * Government/School/Military sales
* User Count: 10
* ~8% of yearly revenue
* Key Technologies:
  * Same as Phone Sales

## 3rd Party Operations
* Major functions:
  * Monitor automated orders from Amazon, Quill, Staples, and other 3rd party integrations
* User Count: 10
* ~3.6% of yearly revenue
* Key Technologies:
  * FswAdmin.com Components (Internal tools with a UI)
      * Pollywog
          * Order review tool for incoming partner EDI orders
          * 3+ years old
  * Scheduled Transmission Processor
     * Backend service that performs many critical tasks including:
          * Processes 3rd Party Purchase Orders
          * Sends Ship Notifications
     * 5+ years old
  * Incoming Transmission Service
     * Backend service that receives new EDI orders from partners
     * 5+ years old

## Customer Service
* Major Functions:
 * Ensure customer satisfaction in ordering and delivery of products
 * Support sales by interacting with warehouse and fulfillers
* User Count: 15
* Key Technologies:
  * Same as Phone Sales +
   * FswAdmin.com Components (Internal tools with a UI)
    * Fulfiller Manager
     * Manage tax, carriers, contacts and other settings by fulfiller
     * 5+ years old
    * Fulfillment Team Order Tracking (FTOT)
     * View and manage the fulfillment status of orders by item
     * 4+ years old
    * Coupon Manager/Coupon Batch Manager
     * Create coupon templates in Coupon Manager
     * Coupon Batch Manager uses those templates to produce coupon codes in batches
     * 5+ years old
    * Scheduled Transmission Processor
     * Backend service
      * Sends ship notifications
     * 5+ years old

## Licensing
* Major functions:
 * Ordering and fulfillment platform for Pride dealers
* User Count: 20
* Key Technologies:
  * Eclipse
     * Dealers can place orders for their customers that are fulfilled by various manufacturers, including FSW
  * Mercury
     * Dealers can place orders with the sole purpose of stocking their individual warehouses
  * Apollo
     * Contains orders placed in both Eclipse and Mercury.  Dealers can edit and send purchase orders to be processed/shipped
  * Helios
     * Displays the status of an order on the project level
  * Fulfiller Manager
     * Dealers are able to define fulfillers for specific manufacturer
  * Brand Manager
     * An internal application that allows us to define addresses for brands and which distributors can fulfill certain brands

## IppBuy
* Major functions:
  * Ordering platform for Pride dealers
* User Count: 5 in Fsw + any dealers using the program
* Vital to business
  * ~37.4% of yearly revenue
* Key Technologies:
  * FswAdmin.com Components (Internal tools with a UI) 
      * (All tools under Partner Tools tab – most of them 2-3 years old)
         * Dealer Contracts
             * Tool for giving dealers access to order Fsw warehoused products by manufacturer
         * Dealer Direct Group Buys
             * Tool for creating and managing Group Buy promotions for dealer orders
         * Fsw Assist Handling Fees
             * Tool for managing handling fees added to dealer orders based on quantity of products ordered
         * Fsw Assist Master Order list
             * Tool used for creating and editing aggregated True purchase orders from both IppBuy.com and Fsw core business
         * IppBuy Dealer Manager
             * Tool for adding and editing dealer profiles and settings
         * IppBuy Freight Invoices
             * Tool for viewing and managing invoices on IppBuy freight orders
         * IppBuy Fulfillers
             * Tool for adding and editing IppBuy fulfillers by manufacturer
         * IppBuy Invoicing
             * Tool for viewing and managing orders ready for invoicing
         * IppBuy Settings
             * Tool for managing settings on a manufacturer by IppBuy program
         * IppBuy Tax Manager
             * Tool for applying tax to IppBuy orders for specific manufacturers by state
         * IppBuy Unverified Queue
             * Orders which require review from the Internal IppBuy team may be viewed here
   * IppBuy.com project (Located in Fsw4.0 solution)
      * Publicly facing website for dealers to create and manage orders
      * 3+ years old
   * Solr Search Service
      * IppBuy product collection search indexer
      * 3+ years old
   * Avalara (3rd party backend service)
      * Unseen 3rd party service/integration for getting tax rates by location a specific location
      * 3+ years old

## Distribution
* Major functions:
 * Fulfillment
 * Shipping
 * Warehouse/Inventory
 * Products
* Key Technologies:
 * FswAdmin.com Components (Internal tools with a UI)
  * WMS Purchase Orders
   * Create and edit outgoing purchase orders for replenishing warehouse inventory
   * 3+ years old
  * Pricing Manager
   * Set default pricing, Unit Of Sale, Sale Incentives and other settings of Skus by manufacturer (Fsw only)
   * 4+ years old
  * Pricing Availability Manager
   * Manage pricing, Unit Of Sale, and other settings of Skus by business partner (Fsw, IPPbuy, Amazon, Staples, Quill, etc)
   * 4+ years old
  * Kit Sku Manager
   * Manage Skus which represent multiple Skus as a single item
    * E.g. Ice Machine Sku + Ice Machine Bin Sku = Single Ice Machine Kit Sku
   * 2+ years old
 * Accellos (3rd party UI)
   * 3rd Party UI and database for managing warehouse inventory and incoming order picking, packing, and shipping
 * NightlyDbUpdates
   * Back end process that performs nightly Inventory updates
   * Performs Moving Average Cost calculation
   * 5+ years old
 * Scheduled Transmission Processor
   * Backend process that provides near real time inventory updates
 * Queue Consumer Service
   * Backend service that handles inventory sync and price change notifications
   * 1 year old
 * TransmissionInConsumer Service
   * Backend service that processes pricing updates in batches from CSV file import
   * 2+ years old
 * Partner Portal
   * Publicly facing website for partner fulfillers to update order status
   * 4+ years old

## Finance
#### Invoicing
* User Count: 10
* Major functions:
 * Invoice dealers
* Key Technologies:
 * Ocr Import
  * Tool for processing digitized paper invoices
  * 5+ years old
 * Invoice Manager (FswAdmin)
  * FswAdmin Tool for viewing and managing core Fsw orders ready for invoicing
   * Recently given UI/performance upgrades
   * 3+ years old
 * Pride Procurement App
  * Tool accounting team uses to handle invoices that have already been sent or are being paid
  * Written in VB6

#### Operations
* User Count: 5
* Major functions:
  * Monitor potentially fraudulent orders across all business domains
   * Fsw.com
   * Phone Sales
   * National Accounts/M&A
 * Approve cancellations/returns/store credit
* Key Technologies:
 * FswAdmin.com Components (Internal tools with a UI)
  * Fraud Queue
   * Queue for viewing and managing orders marked as Potential Fraud
   * 4+ years old
  * Store Credit Manager
   * Tool for managing and approving requests for store credit by order
   * 3+ years old
  * Reimbursements Queue
   * Queue for viewing and managing requests for monetary reimbursement to customers
   * 3+ years old
  * Kount ENS
   * Backend service that receives incoming messages from Kount and updates the Fsw database accordingly
   * 3+ years old
 * Kount Web UI (3rd party UI)
   * 3rd Party web UI for viewing, approving, and declining orders identified as Potential Fraud
   * 3+ years old
 * Avalara (3rd party backend service)
   * Unseen 3rd party service/integration for getting tax rates by location a specific location
   * 3+ years old
 * Paymentech (3rd party backend service)
   * Backend service to validate/authorize credit cards and capture funds
   * Checks newly added customer credit cards for validity
   * 5+++ years old

## OrderUp/Reup
* According to Collin, OrderUp will not be released again and ReUp is dead
* Any orders placed on OrderUp will go to the Unverified Orders Queue to be completed manually by a National Accounts sales representative

Mergers & Acquisitions
* Major functions:
 * Assimilate and integrate dealers/warehouses we purchase into our systems
* ~9.6% of yearly revenue

Reports
* Major functions:
 * Present accurate data
* Key Technologies:
 * CliqView
   * Tool for building reports from data warehouse
   * 1+ year old
 * rpt.foodservicewarehouse.com
   * Internally facing website
   * Displays reports generated from database stored procedures that run overnight
   * Data/reports are questionable
   * 5+++ years old


Revenue data from http://fswqv.foodservicewarehouse.com/qlikview/ “Sales Data Export” report