# Spotify System Design 
Resource : https://newsletter.systemdesign.one/p/spotify-system-design

Requirements: https://newsletter.systemdesign.one/i/174962283/requirements-and-assumptions 

Capacity: https://newsletter.systemdesign.one/i/174962283/capacity-planning

<br>

---

## High Level Architecture 
![Alt](high_lvl_spotify.jpg)

### Mobile App 
- Generic client side implementation, REST API to fetch meta data 
- Cache recently played songs 
- Client streams audio directly from blob storage or CDN using signed URLs
- TODO: Notes for blob storage and CDN


### Load Balancer 


### API Layer 

### SQL DB 

### Blob Storage 