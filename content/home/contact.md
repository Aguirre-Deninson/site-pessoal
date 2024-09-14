---
# An instance of the Contact widget.
widget: contact

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 130

title: Contato
subtitle:

content:
  # Automatically link email and phone or display as text?
  autolink: true

  # Email form provider
  form:
    provider: netlify
    formspree:
      id:
    netlify:
      # Enable CAPTCHA challenge to reduce spam?
      captcha: true

  # Contact details (edit or remove options as required)
  email: 
  phone: 
  address:
    street: 
    city: Goiânia
    region: Goiás
    postcode: ''
    country: Brazil
    country_code: BR
  coordinates:
    latitude: '-16.6809'
    longitude: '-49.2533'
  directions:  
  office_hours:
  appointment_url: ''
  contact_links:
    - icon: linkedin
      icon_pack: fab
      name: DM Me
      link: 'https://www.linkedin.com/in/deninson-aguirre-08437b1b2/'

design:
  columns: '2'
---
