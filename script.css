/* KÍ ỨC THỜI NIÊN THIẾU — tương tác nhẹ, không cần thư viện ngoài */
document.addEventListener("DOMContentLoaded", () => {
  const menuToggle = document.getElementById("menuToggle");
  const mainNav = document.getElementById("mainNav");
  const floatingTop = document.getElementById("floatingTop");

  // Menu điều hướng trên màn hình nhỏ
  menuToggle.addEventListener("click", () => {
    const isOpen = mainNav.classList.toggle("open");
    menuToggle.setAttribute("aria-expanded", String(isOpen));
  });
  mainNav.querySelectorAll("a").forEach(link => {
    link.addEventListener("click", () => {
      mainNav.classList.remove("open");
      menuToggle.setAttribute("aria-expanded", "false");
    });
  });

  // Nút "Về đầu trang" xuất hiện khi cuộn xuống
  const updateTopButton = () => {
    floatingTop.classList.toggle("visible", window.scrollY > 450);
  };
  window.addEventListener("scroll", updateTopButton, { passive: true });
  updateTopButton();
  floatingTop.addEventListener("click", () => {
    window.scrollTo({ top: 0, behavior: "smooth" });
  });

  // Nếu ảnh chưa được thay đường dẫn, hiển thị ô nhắc thay ảnh thay vì biểu tượng ảnh lỗi.
  document.querySelectorAll("img").forEach(img => {
    const isPlaceholder = img.getAttribute("src") === "(hình ảnh cần chèn)";
    if (isPlaceholder) {
      img.dataset.placeholder = "true";
      img.addEventListener("error", () => {
        img.alt = "Hãy thay đường dẫn bằng ảnh của bạn";
        img.classList.add("missing-image");
      });
      img.src = "data:image/gif;base64,R0lGODlhAQABAAD/ACwAAAAAAQABAAACADs=";
      img.classList.add("missing-image");
    }
  });

  // Lightbox: nhấn ảnh trong album để xem lớn, có thể chuyển ảnh trước/sau.
  const lightbox = document.getElementById("lightbox");
  const lightboxImage = document.getElementById("lightboxImage");
  const lightboxCaption = document.getElementById("lightboxCaption");
  const closeButton = document.getElementById("lightboxClose");
  const prevButton = document.getElementById("lightboxPrev");
  const nextButton = document.getElementById("lightboxNext");
  const photos = [...document.querySelectorAll(".photo-card img")];
  let activePhoto = 0;

  function openPhoto(index) {
    activePhoto = (index + photos.length) % photos.length;
    const photo = photos[activePhoto];
    lightboxImage.src = photo.dataset.originalSrc || photo.src;
    lightboxImage.alt = photo.alt;
    lightboxCaption.textContent = photo.closest("figure").querySelector("figcaption")?.textContent || "";
    lightbox.classList.add("open");
    lightbox.setAttribute("aria-hidden", "false");
    document.body.style.overflow = "hidden";
  }
  function closePhoto() {
    lightbox.classList.remove("open");
    lightbox.setAttribute("aria-hidden", "true");
    document.body.style.overflow = "";
  }
  photos.forEach((photo, index) => {
    const original = photo.getAttribute("src");
    if (original && original !== "(hình ảnh cần chèn)") photo.dataset.originalSrc = original;
    photo.closest("figure").addEventListener("click", () => openPhoto(index));
  });
  closeButton.addEventListener("click", closePhoto);
  prevButton.addEventListener("click", () => openPhoto(activePhoto - 1));
  nextButton.addEventListener("click", () => openPhoto(activePhoto + 1));
  lightbox.addEventListener("click", event => {
    if (event.target === lightbox) closePhoto();
  });
  document.addEventListener("keydown", event => {
    if (!lightbox.classList.contains("open")) return;
    if (event.key === "Escape") closePhoto();
    if (event.key === "ArrowLeft") openPhoto(activePhoto - 1);
    if (event.key === "ArrowRight") openPhoto(activePhoto + 1);
  });

  // Video để ở trạng thái trống cho tới khi bạn thay link file .mp4.
  document.querySelectorAll("video source").forEach(source => {
    if (source.getAttribute("src") === "(video cần chèn)") {
      source.removeAttribute("src");
      source.parentElement.load();
    }
  });
});
