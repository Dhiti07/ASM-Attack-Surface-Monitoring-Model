surfacemap

Attack surface scanner with a RAG layer that explains findings in plain English.

Point it at a domain, it finds what's exposed, scans it, and then explains each finding in language someone non-technical can actually act on. The explanations are grounded in CVE data so it cites sources instead of making things up.

Built during my internship at Athenian Tech.

Only scan domains you own or have permission to test.

Modules
Subdomain enumeration
Port scanning
SSL/TLS analysis
Email security (SPF, DKIM, DMARC)
Technology detection
Cybersquatting detection
Cloud asset discovery
Source code leak detection
DNS records
HTTP security headers
WHOIS lookup
Directory discovery
Reputation checks
The RAG bit

Raw scan output is unreadable if you're not a security person. So findings get passed to a retrieval layer that pulls relevant CVE context from a Qdrant vector DB and generates an explanation.

It only answers from what it retrieves, and shows the CVEs it used. Partly to reduce hallucination, partly so you can check its work.

[Add a note here about how you built the CVE index — where the data came from, how you chunked it, what embedding model. This is the most interesting part of the project and right now it's the least documented.]

Stack

Python, FastAPI, Uvicorn, Qdrant, Docker. Frontend is plain HTML/CSS/JS served by FastAPI.

Everything is pure Python, no shelling out to CLI tools, so it runs the same on Windows and Kali.

Setup
bash
git clone https://github.com/Dhiti07/surfacemap.git
cd surfacemap
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env    # fill in your keys
uvicorn main:app --reload

Then open localhost:8000/app.

You'll need a Qdrant instance running. [Add: local docker command or cloud setup, whichever you used.]

Screenshots

[Add 2-3 here. At minimum: the results view, and a finding expanded to show the RAG explanation with citations. This section does more work than everything above it.]

Things that don't work well yet

[Write this yourself, it matters more than it looks. Some starting points from what you've actually hit:

passive subdomain enumeration misses assets
scans on large attack surfaces are slow
whatever the deal was with renderResults not firing after scan completion
anything a module gets wrong or times out on

Be specific. "SSL module times out on hosts that don't respond to SNI" reads like someone who built the thing. "Some modules may have limitations" reads like filler.]
