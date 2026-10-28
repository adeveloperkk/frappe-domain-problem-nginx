# Fix Frappe Domain Pointing to an Old Site

If a domain was previously mapped to another Frappe site on the same VPS, it may continue pointing to the old site even after that site has been deleted. This guide explains how to inspect the Nginx configuration and regenerate it to resolve the issue.

## 🔍 Step 1: Inspect the Nginx Configuration

Replace `yourdomain.com` with your actual domain name.

```bash
sudo grep -R "yourdomain.com" /etc/nginx/sites-enabled/ /etc/nginx/conf.d/ 2>/dev/null
```

This command searches the enabled Nginx configurations for references to your domain.

## ⚙️ Step 2: Regenerate the Nginx Configuration

Navigate to your Frappe Bench directory:

```bash
cd ~/frappe-bench
```

Regenerate the Nginx configuration:

```bash
bench setup nginx
```

## ✅ Step 3: Test the Nginx Configuration

Before reloading Nginx, verify that the configuration is valid:

```bash
sudo nginx -t
```

If the test succeeds, reload Nginx:

```bash
sudo systemctl reload nginx
```

## 🧪 Step 4: Test Domain Routing

Check which site responds to your domain:

```bash
curl -I -H "Host: yourdomain.com" http://127.0.0.1
```

Replace `yourdomain.com` with your actual domain.

If the domain still points to the old site, verify the domain mapping, the current site configuration, and any remaining Nginx server blocks.

## ⚠️ Important Notes

- Run the commands from the correct Frappe Bench directory.
- Make sure the intended site exists before assigning the domain.
- Regenerating Nginx configuration does not automatically remove DNS records or external proxy settings.
- If the issue persists, check for stale Nginx configurations or duplicate domain mappings.
- Always run `sudo nginx -t` before reloading Nginx.

---

## 👨‍💻 Author

Created by **DeveloperKK**

🌐 Website: [https://developerkk.in](https://developerkk.in)

## 💖 Support

**Buy Me a Coffee ☕**

👉 [https://razorpay.me/@elevatebharat](https://razorpay.me/@elevatebharat)

Your support helps create more:

- Frappe tutorials
- ERPNext guides
- DevOps and automation content 🚀

## 💸 Let's Earn Together!

Refer clients and earn **20% commission on every successful project referral**.

## 📞 Need Help?

- 📧 Email: [info@developerkk.in](mailto:info@developerkk.in)
- 🌐 Website: [https://developerkk.in](https://developerkk.in)

## 📄 License

This guide is open-source and free to use for educational and professional purposes.
