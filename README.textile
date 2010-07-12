SocialPoint
========

SocialPoint is a .NET library which allows you to call and work with the Socialtext REST APIs though .NET code. SocialPoint was specifically designed and developed to work within SharePoint but because it is written using the .NET framework 3.0, it can be used within any .NET project.

This project contains the core library and a sample application that demonstrates how to call the Socialtext REST APIs. The core library (Socialtext.SocialPoint.Common) contains all the logic necessary to execute HTTP Web Requests against any of the REST APIs within Socialtext. Simply call the Execute method and pass through any of the REST API URLs defined in the [Socialtext documentation][1]. 



Installation
------------------

The SocialPoint project consists of a standard C# class library and a sample ASP.NET web application. The class library is strongly named and can be placed in the GAC if the library if intended to be used in multiple applications or within SharePoint. 


Examples
-----------
**Code Sample:**
The following code snippet demonstrates a simple GET request for a Socialtext User object using .NET:


    string socialtextServerUrl = "http://socialtext.company.com"; // Server URL of the Socialtext server
    string impersonatorUserId = "userid"; // User ID of the configured impersonator
    string impersonatorPassword = "password"; // Password of the configured impersonator
    string userToFind = "user@company.com"; // ID of the user to get details for
        
    // Initialize a new SocialtextServer object for the Socialtext server
    Socialtext.SocialPoint.Common.Integration.SocialtextServer server = 
        new Socialtext.SocialPoint.Common.Integration.SocialtextServer(socialtextServerUrl);
    
    // Set impersonator user ID and password
    server.MasterID = impersonatorUserId;
    server.MasterPwd = impersonatorPassword;
    
    // Set URL of REST API to call
    string url = "/data/users/" + userToFind;
        
    // Execute GET REST API call
    string stResponse = Socialtext.SocialPoint.Common.SocialtextAPIHelper
        .ProcessUrlRequest(url, server, 
        Socialtext.SocialPoint.Common.Enums.RequestMethod.GET);
    
    // Output JSON response
    Console.WriteLine(stResponse);
    
**Code Sample:**

The following code snippet demonstrates a simple GET request for a Socialtext Group object using .NET:

    string socialtextServerUrl = "http://socialtext.company.com"; // Server URL of the Socialtext server
    string impersonatorUserId = "userid"; // User ID of the configured impersonator
    string impersonatorPassword = "password"; // Password of the configured impersonator
    string groupId = "21"; // ID of the group to get details for
    
    // Initialize a new SocialtextServer object for the Socialtext server
    Socialtext.SocialPoint.Common.Integration.SocialtextServer server =
        new Socialtext.SocialPoint.Common.Integration.SocialtextServer(socialtextServerUrl);
    
    // Set impersonator user ID and password
    server.MasterID = impersonatorUserId;
    server.MasterPwd = impersonatorPassword;
    
    // Set URL of REST API to call
    string url = "/data/groups/" + groupId;
    
    // Execute GET REST API call
    string stResponse = Socialtext.SocialPoint.Common.SocialtextAPIHelper
        .ProcessUrlRequest(url, server, 
        Socialtext.SocialPoint.Common.Enums.RequestMethod.GET);
    
    // Output JSON response
    Console.WriteLine(stResponse);


**Code Sample:**

The following code snippet demonstrates a simple POST request to send a Socialtext Signal using .NET:

string socialtex

    tServerUrl = "http://socialtext.company.com"; // Server URL of the Socialtext server
    string impersonatorUserId = "userid"; // User ID of the configured impersonator
    string impersonatorPassword = "password"; // Password of the configured impersonator
    string groupId = "21"; // ID of the group to send the signal to
    string signalText = "Hello World from .NET"; // Signal to send to Socialtext
    string currentUserId = "user@company.com"; // User ID for the user sending the signal;
    
    // Initialize a new SocialtextServer object for the Socialtext server
    Socialtext.SocialPoint.Common.Integration.SocialtextServer server =
        new Socialtext.SocialPoint.Common.Integration.SocialtextServer(socialtextServerUrl);
    
    // Set impersonator user ID and password
    server.MasterID = impersonatorUserId;
    server.MasterPwd = impersonatorPassword;
    server.IsPublic = false;
    server.UserID = currentUserId;
    
    // Set URL of REST API to call
    string url = "/data/signals";
    
    // Set JSON request body
    string postData = "{\"signal\":\"" + signalText + "\", \"group_ids\":[" + groupId + "]}";
    
    // Execute GET REST API call
    string lastModified;
    string stResponse = Socialtext.SocialPoint.Common.SocialtextAPIHelper
        .ProcessUrlRequest(url, server, 
        Socialtext.SocialPoint.Common.Enums.RequestMethod.POST, postData, out lastModified);
    
    // Output JSON response
    Console.WriteLine(stResponse);


**Code Sample:**

The following code snippet demonstrates serializing a Socialtext REST response of a User object into a .NET object using .NET 3.5 JSON runtime.


    **User Class**
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Runtime.Serialization;
    
    [DataContract]
    public sealed class User
    {
        
        [DataMember(Name = "creator_username", IsRequired = true)]
        public string creator_username { get; set; }
    
        [DataMember(Name = "last_name", IsRequired = true)]
        public string last_name { get; set; }
    
        [DataMember(Name = "primary_account_id", IsRequired = true)]
        public string primary_account_id { get; set; }
    
        [DataMember(Name = "groups", IsRequired = false)]
        public List<Group> groups { get; set; }
    
        [DataMember(Name = "email_address", IsRequired = true)]
        public string email_address { get; set; }
    
        [DataMember(Name = "display_name", IsRequired = true)]
        public string display_name { get; set; }
    
        [DataMember(Name = "username", IsRequired = true)]
        public string username { get; set; }
    
        [DataMember(Name = "created_by_user_id", IsRequired = true)]
        public string created_by_user_id { get; set; }
    
        [DataMember(Name = "primary_account_name", IsRequired = true)]
        public string primary_account_name { get; set; }
    
        [DataMember(Name = "creation_datetime", IsRequired = true)]
        public string creation_datetime { get; set; }
    
        [DataMember(Name = "email_address_at_import", IsRequired = true)]
        public string email_address_at_import { get; set; }
    
        [DataMember(Name = "user_id", IsRequired = true)]
        public string user_id { get; set; }
    
        [DataMember(Name = "first_name", IsRequired = true)]
        public string first_name { get; set; }
    
        [DataMember(Name = "is_business_admin", IsRequired = true)]
        public bool is_business_admin { get; set; }
    
        [DataMember(Name = "is_system_created", IsRequired = true)]
        public bool is_system_created { get; set; }
    
        [DataMember(Name = "is_technical_admin", IsRequired = true)]
        public bool is_technical_admin { get; set; }
    }
    
    **Group Class**
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Runtime.Serialization;
    
    [DataContract]
    public sealed class Group
    {
        [DataMember(Name = "permission_set", IsRequired = true)]
        public string permission_set { get; set; }
    
        [DataMember(Name = "name", IsRequired = true)]
        public string name { get; set; }
    
        [DataMember(Name = "created_by_username", IsRequired = true)]
        public string created_by_username { get; set; }
    
        [DataMember(Name = "description", IsRequired = false)]
        public string description { get; set; }
    
        [DataMember(Name = "account_ids", IsRequired = false)]
        public int[] account_ids { get; set; }
    
        [DataMember(Name = "created_by_user_id", IsRequired = true)]
        public int created_by_user_id { get; set; }
    
        [DataMember(Name = "primary_account_name", IsRequired = true)]
        public string primary_account_name { get; set; }
    
        [DataMember(Name = "primary_account_id", IsRequired = true)]
        public int primary_account_id { get; set; }
    
        [DataMember(Name = "group_id", IsRequired = true)]
        public int group_id { get; set; }
    
        [DataMember(Name = "creation_date", IsRequired = true)]
        public string creation_date { get; set; }
    
        [DataMember(Name = "workspace_count", IsRequired = true)]
        public int workspace_count { get; set; }
    
        [DataMember(Name = "user_count", IsRequired = true)]
        public int user_count { get; set; }
    }
    
    **Processing Code**
    
    string socialtextServerUrl = "http://socialtext.company.com"; // Server URL of the Socialtext server
    string impersonatorUserId = "userid"; // User ID of the configured impersonator
    string impersonatorPassword = "password"; // Password of the configured impersonator
    string userToFind = "user@company.com"; // ID of the user to get details for
    
    // Initialize a new SocialtextServer object for the Socialtext server
    Socialtext.SocialPoint.Common.Integration.SocialtextServer server = 
        new Socialtext.SocialPoint.Common.Integration.SocialtextServer(socialtextServerUrl);
    
    // Set impersonator user ID and password
    server.MasterID = impersonatorUserId;
    server.MasterPwd = impersonatorPassword;
    
    // Set URL of REST API to call
    string url = "/data/users/" + userToFind;
    
    // Execute GET REST API call
    string stResponse = Socialtext.SocialPoint.Common.SocialtextAPIHelper
        .ProcessUrlRequest(url, server, 
        Socialtext.SocialPoint.Common.Enums.RequestMethod.GET);
    
    // Initialize a JSON serializer for the User object
    DataContractJsonSerializer serializer = new DataContractJsonSerializer(typeof(User));
    
    User user;
    using (MemoryStream stream = new MemoryStream(Encoding.UTF8.GetBytes(stResponse)))
    {
        // Read object into new User object
        user = serializer.ReadObject(stream) as User;
        stream.Close();
    }

