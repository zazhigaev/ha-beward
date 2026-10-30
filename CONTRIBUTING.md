# Contribution Guidelines

Contributions to this project are welcome! Whether you are fixing a bug, adding support for other Beward hardware models, or improving the documentation, please feel free to submit issues and pull requests.

## Development Workflow

1. Fork this repository and create your feature branch from `master`.
2. Keep dependencies and hardware protocol definitions synchronized with the [`py-beward`](https://github.com/zazhigaev/py-beward) library.
3. If you add support for new device models or alter endpoints, update the corresponding documentation sections in `README.md`.
4. Ensure code formatting remains consistent.
5. Test changes against hardware or autonomous Python test scripts before opening a pull request.
6. Submit a Pull Request with a clear description of the modifications and tested firmware versions.

## Bug Reports & Feature Requests

Please use GitHub Issues to report problems or propose enhancements:

- **Bug Reports:** Include your hardware model, firmware version (e.g., from `systeminfo_cgi`), Home Assistant version, and relevant debug logs from `custom_components.beward`.
- **New Device Support:** Provide the output of `systeminfo_cgi` and verified working CGI snapshot/event endpoints.

## Credits & License

By contributing to this repository, you agree that your contributions will be licensed under the project's **MIT License**, respecting the original authorship of Andrey "Limych" Khrolenok and the subsequent fork additions.
