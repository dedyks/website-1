---
title: Instalasi Minikube
content_template: templates/task
weight: 20
card:
  name: tasks
  weight: 10
---

{{% capture overview %}}

Halaman ini menunjukkan cara untuk instalasi [Minikube](/id/docs/tutorials/hello-minikube), sebuah alat untuk menjalankan sebuah *node* tunggal Kubernetes klaster di mesin virtual yang ada di komputer kamu.

{{% /capture %}}

{{% capture prerequisites %}}

{{< tabs name="minikube_before_you_begin" >}}
{{% tab name="Linux" %}}
Untuk mengecek apabila virtualisasi didukung di Linux, jalankan perintah berikut dan pastikan keluarannya tidak kosong:
```
grep -E --color 'vmx|svm' /proc/cpuinfo
```
{{% /tab %}}

{{% tab name="macOS" %}}
Untuk mengecek apabila virtualisasi didukung di Linux, jalankan perintah berikut di terminal kamu.
```
sysctl -a | grep -E --color 'machdep.cpu.features|VMX'
```
Apabila kamu melihat `VMX` pada hasil keluaran (berwarna), artinya fitur VT-x sudah diaktifkan di mesin kamu.
{{% /tab %}}

{{% tab name="Windows" %}}
Untuk mengecek apabila virtualisasi didukung di Windows 8 dan keatas, jalankan perintah berikut di terminal Windows atau *command prompt* kamu.

```
systeminfo
```
Apabila kamu melihat keluaran berikut, virtualisasi didukung di Windows.
```
Hyper-V Requirements:     VM Monitor Mode Extensions: Yes
                          Virtualization Enabled In Firmware: Yes
                          Second Level Address Translation: Yes
                          Data Execution Prevention Available: Yes
```
Apabila kamu melihat keluaran berikut, sistem kamu sudah memiliki sebuah Hypervisor yang telah terinstal dan kamu bisa melewati langkap berikutnya.
```
Hyper-V Requirements:     A hypervisor has been detected. Features required for Hyper-V will not be displayed.
```


{{% /tab %}}
{{< /tabs >}}

{{% /capture %}}

{{% capture steps %}}

# Menginstal minikube

{{< tabs name="tab_with_md" >}}
{{% tab name="Linux" %}}

### Instalasi kubectl

Pastikan kamu mempunyai kubectl terinstal. Kamu bisa menginstal kubectl berdasarkan instruksi di [Instalasi dan Mempersiapkan kubectl](/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux).

### Instalasi sebuah Hypervisor

Apabila kamu belum menginstal sebuah Hypervisor, Instalasi salah satu sekarang:

• [KVM](https://www.linux-kvm.org/), yang menggunakan QEMU

• [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Minikube juga mendukung sebuah opsi `--driver=none` untuk menjalankan komponen - komponen Kubernetes diatas *host* dan tidak didalam VM. Untuk menggunakan *driver* ini memerlukan [Docker](https://www.docker.com/products/docker-desktop) dan sebuah lingkungan Linux bukan sebuah hypervisor.

Apabila kamu menggunakan `none` *driver* di Debian atau turunannya, gunakan  paket `.deb` untuk Docker daripada menggunakan paket *snap*, karena paket *snap* tidak berfungsi dengan Minikube.
Kamu bisa mengunduh paket `.deb` dari [Docker](https://www.docker.com/products/docker-desktop).

{{< caution >}}
*Driver* VM `none` dapat menyebabkan masalah pada keamanan dan kehilangan data. Sebelum menggunakan *driver* VM, periksa [dokumentasi ini](https://minikube.sigs.k8s.io/docs/reference/drivers/none/) untuk informasi lebih lanjut.
{{< /caution >}}

Minikube juga mendukung opsi `vm-driver=podman` yang mirip dengan *driver* Docker. Podman yang berjalan dengan hak istimewa *superuser* adalah cara terbaik untuk memastikan kontainer - kontainer kamu memiliki akses penuh ke semua fitur yang ada di sistem kamu..

{{< caution >}}
*Driver* `podman` memerlukan *root* untuk menjalankan kontainer karena akun pengguna reguler tidak memiliki akses penuh ke semua fitur sistem operasi yang mungkin kontainer perlukan.
{{< /caution >}}

### Instalasi Minikube menggunakan paket

Tersedia paket *experimental* untuk Minikube, kamu bisa menemukan paket untuk Linux (AMD64) dari halaman  [*releases*](https://github.com/kubernetes/minikube/releases) Minikube di GitHub.

Gunakan alat distribusi paket Linux kamu untuk menginstal paket yang sesuai.

### Instalasi Minikube malalui unduh langsung

Jika kamu tidak menginstal melalui sebuah paket, kamu bisa mengunduh sebuah *stand-alone binary* dan menggunakannya.


```shell
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
```

Berikut adalah cara mudah untuk menambahkan *executable* Minikube ke *path* kamu.

```shell
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/
```

### Instalasi Minikube menggunakan Homebrew

Sebagai alternatif lain, kamu bisa menginstal Minikube menggunakan Linux [Homebrew](https://docs.brew.sh/Homebrew-on-Linux):

```shell
brew install minikube
```

{{% /tab %}}
{{% tab name="macOS" %}}
### Instalasi kubectl

Pastikan kamu mempunyai kubectl terinstal. Kamu bisa menginstal kubectl berdasarkan instruksi di [Instalasi dan Mempersiapkan kubectl](/docs/tasks/tools/install-kubectl/#install-kubectl-on-macos).

### Instalasi sebuah Hypervisor

Apabila kamu belum memiliki sebuah Hypervisor terinstal, Instalasi salah satu sekarang:

• [HyperKit](https://github.com/moby/hyperkit)

• [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

• [VMware Fusion](https://www.vmware.com/products/fusion)

### Instalasi Minikube
Cara paling mudah untuk menginstal Minikube di macOS adalah menggunakan [Homebrew](https://brew.sh):

```shell
brew install minikube
```

Kamu juga bisa menginstalnya dengan mengunduh *stand-alone binary*:

```shell
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-darwin-amd64 \
  && chmod +x minikube
```

Berikut adalah cara mudah untuk menambahkan *executable* Minikube ke *path* kamu.

```shell
sudo mv minikube /usr/local/bin
```

{{% /tab %}}
{{% tab name="Windows" %}}
### Instalasi kubectl

Pastikan kamu mempunyai kubectl terinstal. Kamu bisa menginstal kubectl berdasarkan instruksi di [Instalasi dan Mempersiapkan kubectl](/docs/tasks/tools/install-kubectl/#install-kubectl-on-windows).

### Instalasi sebuah Hypervisor

Apabila kamu belum memiliki sebuah Hypervisor terinstal, Instalasi salah satu sekarang:

• [Hyper-V](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/quick_start/walkthrough_install)

• [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

{{< note >}}
Hyper-V hanya dapat berjalan diatas tiga versi Windws 10: Windows 10 Enterprise, Windows 10 Professional, dan Windows 10 Education.
{{< /note >}}

### Instalasi Minikube menggunakan Chocolatey

Cara paling mudah untuk menginstal Minikube di Windows adalah menggunakan [Chocolatey](https://chocolatey.org/) (jalankan sebagai administrator):

```shell
choco install minikube
```

Setelah Minikube telah selesai diinstal. tutup sesi *CLI* dan matikan ulang. Minikube akan ditambahkan ke *path* kamu secara otomatis.

### Instalasi Minikube menggunakan sebuah *installer executable*

Untuk menginstal Minikube secara manual di Windows menggunakan [Windows Installer](https://docs.microsoft.com/en-us/windows/desktop/msi/windows-installer-portal), unduh [`minikube-installer.exe`](https://github.com/kubernetes/minikube/releases/latest/download/minikube-installer.exe) dan jalankan *installer*.

### Installasi Minikube melalui unduh langsung

Untuk menginstal Minikube secara manual di Windows, unduh [`minikube-windows-amd64`](https://github.com/kubernetes/minikube/releases/latest), ubah nama menjadi `minikube.exe`, dan tambahkan ke *path* kamu.

{{% /tab %}}
{{< /tabs >}}


{{% /capture %}}

{{% capture whatsnext %}}

* [Menjalanakan Kubernetes secara lokal dengan Minikube](/docs/setup/learning-environment/minikube/)

{{% /capture %}}

## Memastikan instalasi

Untuk memastikan keberhasilan kedua instalasi hypervisor dan Minikube, kamu bisa menjalankan perintah berikut untuk memulai klaster Kubernetes lokal:
{{< note >}}

Untuk pengaturan  `--driver` dengan `minikube start`, masukkan nama hypervisor `<driver_name>` yang kamu instal dengan huruf kecil seperti yang ditunjukan dibawah. Daftar lengkap nilai `--driver` tersedia di [dokumentasi menentukan *driver* VM](https://kubernetes.io/docs/setup/learning-environment/minikube/#specifying-the-vm-driver).

{{< /note >}}

```shell
minikube start --driver=<driver_name>
```

Setalah `minikube start` selesai, jalankan perintah dibawah untuk mengecek status klaster:

```shell
minikube status
```

Jika klaster berjalan, keluaran dari `minikube status` akan mirip seperti ini:

```
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```

Setelah kamu memastikan bahwa Minikube berjalan sesuai dengan hypervisor yang telah kamu pilih, kamu dapat melanjutkan untuk memakai Minikube atau menghentikan klaster kamu. Untuk menghentikan klaster, jalankan:

```shell
minikube stop
```

## Membersihkan *state* lokal {#cleanup-local-state}

Jika sebelumnya kamu pernah menginstal Minikube, dan menjalankan:
```shell
minikube start
```

dan `minikube start` memberikan *error*:
```
machine does not exist
```

maka kamu dapat membersihkan lokal *state* minikube:
then you need to clear minikube's local state:
```shell
minikube delete
```
