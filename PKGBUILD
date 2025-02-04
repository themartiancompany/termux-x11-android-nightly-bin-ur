# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_fdroid="false"
_github="true"
_system_install="false"
_user_install="true"
if [[ "${_system_install}" == "true" ]]; then
  _install_type="system"
elif [[ "${_user_install}" == "true" ]]; then
  _install_type="user"
fi
_offline="false"
_git="false"
_proj="hip"
_pkg="termux"
_component="x11"
_variant="nightly"
_pkgbase="${_pkg}-${_component}"
_pkgname="${_pkgbase}"
_app_id="com.${_pkg}"
_Pkg="Termux-X11"
pkgname=(
  "${_pkgname}-android-${_variant}-bin"
)
pkgver=1.03.1.2025.01.29
# _commit="e117ccae32d5a7d75479b61f034000122fe9fa24"
_fdroid_pkgrel=1000
pkgrel=1
if [[ "${_fdroid}" == "true" ]]; then
  pkgrel="${_fdroid_pkgrel}"
fi
_pkgdesc=(
  "Termux X11 add-on application."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'arm'
  'aarch64'
  'x86_64'
  'i686'
)
_arch="$( \
  uname \
    -m)"
_aarch="${_arch}"
if [[ "${_arch}" == "armv7l" ]]; then
  _aarch="armeabi-v7a"
elif [[ "${_arch}" == "aarch64" ]]; then
  _aarch="arm64-v8a"
fi
url="${_pkgname}.dev"
license=(
  'GPL3'
)
depends=(
  "${_pkgbase}-${_variant}"
)
_os="$( \
  uname \
    -o)"
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  depends+=(
    'inteppacman'
  )
optdepends=(
)
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  optdepends+=(
  )
makedepends=(
  'coreutils'
)
checkdepends=(
)
provides=(
  "${_pkgname}-android-bin=${pkgver}"
  "${_pkgname}-android=${pkgver}"
)
conflicts=(
  "${_pkgname}-android-bin"
  "${_pkgname}-android"
)
source=()
sha256sums=()
_fdroid_url="https://f-droid.org/repo"
_http="https://github.com"
_ns="${_pkg}"
_github_url="${_http}/${_ns}/${_pkgname}"
# _tag="${pkgrel}"
# _tag="${pkgver}"
_tag="nightly"
# _tag_name="pkgrel"
_tag_name="pkgver"
_tarname="${_pkgname}-${pkgver}-${pkgrel}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${pkgname}"
source=()
sha256sums=()
if [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}"
  _sum="SKIP"
elif [[ "${_git}" == false ]]; then
  if [[ "${_fdroid}" == "true" ]]; then
    _url="${_fdroid_url}"
    if [[ "${_tag_name}" == 'pkgrel' ]]; then
      _src="${_tarname}.apk::${_url}/${_pkg}_${pkgrel}.apk"
      _sig="${_tarname}.apk.sig::${_url}/${_pkg}_${pkgrel}.apk.asc"
      source+=(
        "${_sig}"
      )
      sha256sums+=(
        "SKIP"
      )
      _sum="f137958392a800fca583bfc00f191b8edb29b77c705fddf27dffb6c26ca5d413"
    fi
  elif [[ "${_github}" == "true" ]]; then
    _url="${_github_url}"
    if [[ "${_tag_name}" == "pkgver" ]]; then
      _dl_name="app-${_aarch}-debug.apk"
      _src="${_tarname}.apk::${_url}/releases/download/${_tag}/${_dl_name}"
      if [[ "${_aarch}" == "arm64-v8a" ]]; then
        _sum="72c8d3cf7cb12d8c550a6b2750bd00bc99ad084c70f8ff0d2ffa9189e685ce4f"
      elif [[ "${_aarch}" == "armeabi-v7a" ]]; then
        _sum="7bc622d07142687bceee963752e5a0b2a862a6c6f2baf447aad1075b0ddebd70"
        _sum="SKIP" # <- this will have to stay I guess for this package.
      elif [[ "${_aarch}" == "x86" ]]; then
        _sum="084ada98b58d28e9df38b234afb8653a53e37a237e7446e3e3077c68c5281b7c"
      elif [[ "${_aarch}" == "x86_64" ]]; then
        _sum="cc63b1cda554adf84a152f99703847871790943fb0ce492ec6d200bd0bec2dc6"
      fi
    elif [[ "${_tag_name}" == "commit" ]]; then
      _src="${_tarname}.zip::${_url}/archive/${_commit}.zip"
      _sum="dacf4a05e8dab38c49034e5d58deb477c36d005fe81324cf7973ba5487d87eb7"
    fi
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
noextract=(
  "${_src}"
)
validgpgkeys=(
  # F-droid binary releases
  "37D2C98789D8311948394E3E41E7044E1DBA2E89"
)

package() {
  local \
    _dest_dir \
    _dest \
    _extra_libs=() \
    _manifest \
    _manifests=() \
    _lib
  _dest_dir="/usr/bin"
  _dest="${_pkgname}.apk"
  if [[ "${_os}" == "Android" ]]; then
    if [[ "${_install_type}" == "system" ]]; then
      _dest_dir="/system/app/${_Pkg}"
    elif [[ "${_install_type}" == "user" ]]; then
      _dest_dir="/data/app/${_app_id}"
    fi
    _dest="base.apk"
  fi
  install \
    -dm755 \
    "${pkgdir}${_dest_dir}"
  install \
    -Dm644 \
    "${srcdir}/${_tarname}.apk" \
    "${pkgdir}${_dest_dir}/${_dest}"
}

# vim: ft=sh syn=sh et
