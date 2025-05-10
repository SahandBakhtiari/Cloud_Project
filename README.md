
# 📝 To-Do App - Fullstack with Flask, Docker & Kubernetes

یک اپلیکیشن ساده و کامل To-Do List با API بک‌اند در Flask، رابط کاربری زیبا، قابلیت اجرا در Docker، دیپلوی در Kubernetes، و مجهز به CI با GitHub Actions.

---

## 📸 پیش‌نمایش رابط کاربری

تصوبر زیر نمایی از رابط کاربری پروژه هست:


![image](https://github.com/user-attachments/assets/45acbba9-7dfe-42d1-84a9-e3c73761a3bf)


## ⚙️ ویژگی‌ها

* رابط کاربری ساده، مدرن و واکنش‌گرا با طراحی راست‌به‌چپ (RTL)
* API کامل RESTful با استفاده از Flask
* مسیرهای API:

  * GET /tasks
  * POST /tasks
  * GET /tasks/<id>
  * DELETE /tasks/<id>
* اتصال آینده‌نگر به MongoDB (در حال حاضر in-memory)
* سرویس Health Check در /health
* Dockerfile جهت ساخت کانتینر
* Deployment روی Kubernetes (Minikube)
* Liveness و Readiness Probe
* CI با GitHub Actions برای Build و Push ایمیج Docker

---

## 🧪 اجرای پروژه به‌صورت محلی

۱. نصب وابستگی‌ها:

```bash
pip install flask
```

۲. اجرای پروژه:

```bash
python app.py
```

۳. مرورگر را باز کن و وارد آدرس زیر شو:

```
http://localhost:5000
```

---

## 🐳 اجرای پروژه با Docker

۱. ساخت ایمیج:

```bash
docker build -t todo-app .
```

۲. اجرای کانتینر:

```bash
docker run -p 5000:5000 todo-app
```

---

## ☸️ استقرار در Kubernetes با Minikube

۱. اجرای Minikube:

```bash
minikube start --driver=docker
```

۲. اعمال manifestها:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

۳. باز کردن سرویس در مرورگر:

```bash
minikube service todo-service
```

---

## 🔁 مقیاس‌پذیری و Probeها

📌 Manual Scaling:

```bash
kubectl scale deployment todo-app --replicas=3
```

![image](https://github.com/user-attachments/assets/2d9bec13-2069-435b-a222-dc71001b2699)



📌 Auto Scaling:

```bash
kubectl autoscale deployment todo-app --cpu-percent=50 --min=2 --max=5
```

![image](https://github.com/user-attachments/assets/f901654f-8ae8-46c5-a53b-6335e0131f4b)


📌 Liveness / Readiness Probe (در deployment.yaml):

```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 5000
  initialDelaySeconds: 5
  periodSeconds: 10

readinessProbe:
  httpGet:
    path: /health
    port: 5000
  initialDelaySeconds: 3
  periodSeconds: 5
```

![image](https://github.com/user-attachments/assets/d702359f-1ecd-456f-965a-c9c4fdc97476)


---

## 🚀 CI با GitHub Actions

هر بار که push به main انجام بشه:

* ایمیج Docker ساخته می‌شه
* در Docker Hub منتشر می‌شه

📂 مسیر فایل CI:

.github/workflows/docker.yml

🔒 Secrets موردنیاز:

* DOCKER\_USERNAME
* DOCKER\_PASSWORD

---

## 🗂 ساختار پروژه

```
todo-app/
├── app.py
├── Dockerfile
├── requirements.txt
├── deployment.yaml
├── service.yaml
├── templates/
│   └── index.html
├── static/
│   └── style.css
├── .github/
│   └── workflows/
│       └── docker.yml
├── README.md
```

---

## ✅ برنامه‌های آینده (TODO)

* اتصال به MongoDB واقعی
* احراز هویت کاربر و حساب کاربری
* ساخت نسخه واکنش‌گرا (Responsive)
* Helm Chart برای دیپلوی آسان‌تر
* اضافه کردن تست‌های خودکار (unit tests)

---

🎯 طراحی و توسعه توسط \[sahand bakhtiari]

لینک پروژه در Docker Hub: [docker.io/sahandbakhtiari/todo-app](https://hub.docker.com/)

---


