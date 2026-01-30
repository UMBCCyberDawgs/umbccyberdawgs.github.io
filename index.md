---
layout: default
---

## Welcome!
Welcome to the UMBC CyberDawgs homepage! We are a group of UMBC students who share a common interest in cybersecurity and good security practices in all aspects of computing.

## Next Events
<ul id="events">Loading events...</ul>

<script>
async function loadEvents() {
    //Access the new list with id "events"
    const list = document.getElementById("events");
    list.innerHTML = "Loading events...";

    try {
        //Request the api for upcoming events
        const res = await fetch("https://api.sga.umbc.edu/events/group/umbccd");
        if (!res.ok) throw new Error("Network response was not ok");
            const text = await res.text();
            const parser = new DOMParser();
            const xml = parser.parseFromString(text, "application/xml");

        //Access each element needed, "Summary" is also available if we want to add that
        const events = [...xml.querySelectorAll("Event")].map(ev => ({
            title: ev.querySelector("Title")?.textContent || "No title",
            link: ev.getAttribute("url") || "#",
            date: ev.querySelector("StartDate")?.textContent || "No start date",
            endDate: ev.querySelector("EndDate")?.textContent || "No end date",
            location: ev.querySelector("Location")?.textContent || "Location TBA"
    }));

    //Clear events from list
    list.innerHTML = "";

    //Check if there are no upcoming events
    if (events.length === 0) {
        list.innerHTML = "<li>No upcoming events</li>";
        return;
    }

    //Helper function to stylize date using js date object
    const formatDateTime = (startStr, endStr) => {
        const start = new Date(startStr);
        const end = new Date(endStr);

        const optionsDate = { weekday: 'long', month: 'long', day: 'numeric', year: 'numeric' };
        const optionsTime = { hour: 'numeric', hour12: true };

        //Format date
        const datePart = start.toLocaleDateString('en-US', optionsDate);

        //Format times
        const startTime = start.toLocaleTimeString('en-US', optionsTime);
        const endTime = end.toLocaleTimeString('en-US', optionsTime);

        return `${datePart} · ${startTime} - ${endTime}`;
    };

    //Display each event element
    events.forEach(ev => {

        const li = document.createElement("li");
        //Create HTML elements for each part of event
        //Also makes the title link back to the original umbc post
        li.innerHTML = `
        <strong><a href="${ev.link}" target="_blank">${ev.title}</a></strong><br>
        <strong>Date:</strong> ${formatDateTime(ev.date, ev.endDate)}<br>
        <strong>Location:</strong> ${ev.location}<br>
        `;
        //Add event to list
        list.appendChild(li);
    });

  } catch (err) {
    console.error("Failed to load events:", err);
    list.innerHTML = "<li>Could not load events at this time</li>";
  }
}

loadEvents();
</script>

## How To Get Involved

You can do a few things to get involved with the club.

1. Join our [Discord](https://discord.gg/hUVkGvvY2y)!
2. Follow our [myUMBC](https://my3.my.umbc.edu/groups/umbccd) page
3. Attend our weekly [meetings](#meetings)
    * Meeting location for the Fall 2025 semester TBA with a hybrid/virtual option on [Webex](https://umbc.webex.com/meet/CyberDawgs)
    * Meeting time is every Monday 7:15pm - 8:15pm
    * Meeting Slides and Recordings will be shared (when possible)

## <a name="meetings">Meetings

We hold general club meetings every Monday from 7:15 to 8:15 PM.
We encourage anyone who wants to learn more about cyber security and develop skills in the field to attend our meetings. If you’re new to cyber or computing security, no worries, you can still come. Although cybersecurity can be difficult at times, it's nowhere near as hard as some people say, so don’t be scared away or discouraged.

No prior experience is required to attend or participate in our meetings.

**What To Expect From A Meeting:**

* An environment conducive to learning relevant tools and techniques
* A place to meet like-minded students and discuss all things cyber and computing security

Our meetings vary in subject material from week to week. If you want to learn more about specific topics, please email our club secretary. If you would like to present a talk or teach a new skill, please email our club president.

## Club Events

Along with our normal club meetings, we also provide great opportunities for
individuals interested in learning about and participating in cyber-related competitions. Here's what we're doing:

* We host two CTF (Capture the Flag) events at UMBC every year:
   * **DawgCTF** Open to all UMBC students of all skill levels. Held during the Spring semester. [Learn more](/dawgctf).
    * **CyberPaws CTF** Open to our club members; aimed at beginners. Challenges are released weekly during the Fall/Spring semester.

* We host a [**Cyber Defense Exercise (CDE)**](/cde) each Fall. CDE is a Red/Blue cyber defense exercise. It is open to all UMBC students and is a great opportunity to learn more about cyber security and cyber competitions. We strongly recommend participating so you can get a taste of the competition environment, in case you'd like to try out for the team.

* To break from the technical jargon, we hold a **Cyber Movie Night** once each semester during a club meeting. We offer free pizza, popcorn, and drinks. These nights are great for hanging out with fellow club members and relaxing from the stress of school.

* Finally, we host an **End-of-Semester Celebration**, each Spring and Fall, for all UMBC students to attend and take a break before exams. We provide pizza, drinks, and candy as well as music and games. We also announce winners of our CTFs and hand out prizes!

## <a name="finishes">Cyber Competition Team</a>

Some of our club members try out for and compete together on a collegiate cyber security competition team. We compete under the same “CyberDawgs” name.

### Planned Competitions
* [DoE Cyberforce](https://cyberforcecompetition.com/)
* [CSAW CTF](https://www.csaw.io/ctf)
* [MACCDC](https://maccdc.org/)
* [ISTS](https://ists.io/)
* [NCL](https://nationalcyberleague.org/competition)
* [MDC3](https://www.fbcconferences.com/e/cybermdconference/challenge.aspx)
* Miscellaneous CTFs

### Team History
[View past competition rankings](/history)

## Contact Information

### Board

**President:** Alex Henning (ahennin1 @ umbc.edu)<br>
**Vice President:** Charles Maxa (cmaxa1 @ umbc.edu)<br>
**Treasurer:** Gabriela Jurado Fuentes (g189 @ umbc.edu)<br>
**Secretary:** Hamza Nasher-Alneam (hnasher1 @ umbc.edu)<br>

### UMBC Liaisons

**Faculty Advisor:** Dr. Charles Nicholas (nicholas @ umbc.edu)<br>
Professor, Department of Computer Science and Electrical Engineering<br>
Affiliate Professor, Department of Information Systems<br>
Director, Graduate Computer Science Programs<br>

**Faculty Advisor:** RJ Joyce (joyce8 @ umbc.edu)<br>
Assistant Teaching Professor, Department of Computer Science and Electrical Engineering<br>

**Team Faculty Advisor:** Kevin Chen (kevin.chen @ umbc.edu)<br>
Professor, Department of Computer Science and Electrical Engineering<br>

# Thank you to our Sponsors and Supporters!
## Gold Tier
(Contact Club Board if Interested!)

## Silver Tier
## <img src="/images/EITLogo.png" height="60%" width="60%">
## <img src="/images/LMLogo.png" height="60%" width="60%">

## Bronze Tier
(Contact Club Board if Interested!)

## Supporters
## <img src="/images/NGLogo.png" height="30%" width="30%">

## Want to see your name here?
Check out the 
[Spring 2026 CyberDawgs Sponsorship Packet](documents/sponsorship-packet-spring-2026.pdf)
<br/><br/>
